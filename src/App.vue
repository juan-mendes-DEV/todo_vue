<script setup>
  import { reactive } from 'vue';

  const estado = reactive({
    filtro:'todas',
    tarefaTemp:'',
    tarefas:[
      {
        titulo: 'Estudar ES6',
        finalizada:false,
      },
      {
        titulo: 'Estudar SASS',
        finalizada:false,
      },
      {
        titulo: 'ir para academia',
        finalizada:true,
      }
    ]
  })


  const getTarefasPendentes = () =>{
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }


  const getTarefasFinalizadas = ()=>{
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }


  const getTarefasFiltradas = () =>{
    const filtro = estado.filtro;
    switch(filtro){
      case 'pendentes':
        return [...getTarefasPendentes()];
      case 'finalizadas':
        return [...getTarefasFinalizadas()];
      default:
        return [...estado.tarefas]
    }
  }

  const cadastraTarefa = ()=>{
    const tarefaNova ={
      titulo: estado.tarefaTemp,
      finalizada:false,
    }
    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp='';
  }
</script>







<template>
  <div class="container">
    <header class="p-5 mb-4 bg-primary rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa" class="bg-primary p-5">
      <div class="row ">
        <div class="col">
          <input :value="estado.taredaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required class="form-control" type="text" placeholder="digite aqui a descrição da tarefa">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-dark">cadastrar</button>
        </div>
        <div class="col-md-2 ">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control bg-light">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <!-- {{ estado.filtro }} -->
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked"  :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{done:tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>

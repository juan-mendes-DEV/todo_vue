<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import Listadetarefas from './components/Listadetarefas.vue'

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
   <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
   <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
   <Listadetarefas :tarefas="getTarefasFiltradas()"/>

  
  </div>
</template>


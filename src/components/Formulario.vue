<script setup>
    const props = defineProps(['cadastraTarefa','tarefaTemp','trocarFiltro','editaTarefaTemp'])

</script>

<template>
    <form @submit.prevent="props.cadastraTarefa" class="bg-primary p-5">
      <div class="row ">
        <div class="col">
          <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required class="form-control" type="text" placeholder="digite aqui a descrição da tarefa">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-dark">cadastrar</button>
        </div>
        <div class="col-md-2 ">
          <select @change="props.trocarFiltro" class="form-control bg-light">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
</template>
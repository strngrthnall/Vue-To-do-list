<script setup>
const props = defineProps([
  'adicionaNovaTarefa',
  'removeFinalizadas',
  'tarefaTemp',
  'editaTarefaTemp',
  'trocarFiltro'
])
</script>
<template>
  <form @submit.prevent="props.adicionaNovaTarefa" @reset.prevent="props.removeFinalizadas">
    <div class="row">
      <div class="col">
        <input 
          required
          type="text" 
          placeholder="Nova tarefa"
          class="form-control"
          @change="props.editaTarefaTemp"
          :value="props.tarefaTemp"
        >
      </div>
      <div class="col-md-2">
        <button 
          class="btn btn-primary ps-4 pe-4"
          type="submit"
        >
          Cadastrar
        </button>
      </div>
      <div class="col-md-2">
        <button 
          class="btn btn-danger ps-4 pe-4"
          type="reset"
        >
          Apagar 
        </button>
      </div>
      <div class="col-md-2">
        <select @change="props.trocarFiltro" class="form-control">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>
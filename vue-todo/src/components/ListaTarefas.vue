<script setup>
const props = defineProps(['tarefas', 'filtro'])
</script>

<template>
  <ul v-if="props.tarefas.length > 0" class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in props.tarefas">
      <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
        :id="tarefa.titulo" type="checkbox">
      <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
  <div class="mt-4" v-else>
    <span  v-if="props.filtro=='todas'"> 
      Nenhuma tarefa cadastrada.
    </span>
    <span v-else-if="props.filtro=='finalizadas'"> 
      Nenhuma tarefa finalizada.
    </span>
    <span v-else> 
        Nenhuma tarefa pendente.
      </span>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
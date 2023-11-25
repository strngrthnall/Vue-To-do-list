<script setup>
import { reactive } from 'vue'
const estado = reactive({
  tarefas: [
    
  ],
  filtro: 'todas',
  tarefaTemp: ''
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();

    case 'finalizadas':
      return getTarefasFinalizadas();

    default:
      return estado.tarefas;
  }
}

const adicionaNovaTarefa = () => {
  const novaTarefa = {
    titulo: estado.tarefaTemp,
    finalizada: false
  }

  estado.tarefas.push(novaTarefa);
  estado.tarefaTemp = ''

}

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p> Existem {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>
      <form @submit.prevent="adicionaNovaTarefa">
      <div class="row">
        <div class="col">
          <input 
            required
            type="text" 
            placeholder="Nova tarefa"
            class="form-control"
            @change="evento => estado.tarefaTemp = evento.target.value"
            :value="estado.tarefaTemp"
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
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>

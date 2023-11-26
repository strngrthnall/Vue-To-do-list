<script setup>
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaTarefas from './components/ListaTarefas.vue'
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
      return  estado.tarefas;
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

const removeFinalizadas = () => {
  estado.tarefas.forEach((tarefa) => {
    if (tarefa.finalizada == true) {
      estado.tarefas.pop(tarefa)
    }
  })
}

</script>

<template>
  <div class="container">
      <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
      <Formulario 
        :tarefa-temp="estado.tarefaTemp"
        :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value"
        :adiciona-nova-tarefa="adicionaNovaTarefa"
        :remove-finalizadas="removeFinalizadas"
        :trocar-filtro="evento => estado.filtro = evento.target.value"
        />
      <ListaTarefas 
        :tarefas="getTarefasFiltradas()"
        :filtro="estado.filtro"
      />
  </div>
</template>



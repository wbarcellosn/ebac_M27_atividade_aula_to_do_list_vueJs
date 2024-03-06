<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive({
  tarefaTemp: '',
  tarefas: [
    
  ],
  filtro: 'todas'
})

const cadastraTarefa = () => {
  const novaTarefa = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }

  estado.tarefas.push(novaTarefa);
  estado.tarefaTemp = '';
}

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada);
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada);
}

const getTarefasFiltradas = () => {
  const filtro = estado.filtro;

  switch (filtro) {
    case 'pendentes': return getTarefasPendentes();
    case 'finalizadas': return getTarefasFinalizadas();
    default: return estado.tarefas;
  }
}

</script>

<template>
  <div class="container">
    <Cabecalho 
    :tarefas-pendentes="getTarefasPendentes().length" 
    />
    <Formulario 
    :tarefa-temp="estado.tarefaTemp"
    :edita-tarefa-temp="e => estado.tarefaTemp = e.target.value"
    :cadastra-tarefa="cadastraTarefa"
    :trocar-filtro="e => estado.filtro = e.target.value" 
    />
    <ListaDeTarefas 
    :tarefas="getTarefasFiltradas()"
    />   
  </div>
</template>

<style scoped>

</style>

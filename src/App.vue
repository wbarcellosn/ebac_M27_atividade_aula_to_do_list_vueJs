<script setup>
import { reactive } from 'vue';

const estado = reactive({
  tarefaTemp: '',
  tarefas: [
   {
    titulo: 'Estudar VueJs',
    finalizada: false,
    },
    {
    titulo: 'Estudar SASS',
    finalizada: false,
    },
    {
    titulo: 'Estudar Js',
    finalizada: false,
    }
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
    <header class="p-5 my-4 bg-light roudend-3">
      <h1 >Minhas Tarefas</h1>
      <p>Você possui {{getTarefasPendentes().length}} tarefas pendentes.</p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="e => estado.tarefaTemp = e.target.value" class="form-control" type="text" placeholder="Digite aqui a sua tarefa" required>
        </div>
        <div class="col-md-1">
          <button class="btn btn-primary" type="submit" >Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="e => estado.filtro = e.target.value" class="form-control">
            <option value="todas">Todas as Tarefas</option>
            <option value="pendentes">Tarefas Pendentes</option>
            <option value="finalizadas">Tarefas Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="e => tarefa.finalizada = e.target.checked" type="checkbox" :checked="tarefa.finalizada" :id="tarefa.titulo">
        <label :class="{concluida: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">{{tarefa.titulo}}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .concluida {
    text-decoration: line-through;
  }
</style>

<script setup>
 const props = defineProps(['tarefas'])
</script>

<template>
  <div>
      <ul class="list-group mt-4" v-if="props.tarefas.length > 0">
          <li class="list-group-item" v-for="tarefa in props.tarefas">
              <input @change="e => tarefa.finalizada = e.target.checked" type="checkbox" :checked="tarefa.finalizada" :id="tarefa.titulo">
              <label :class="{concluida: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">{{tarefa.titulo}}</label>
          </li>
      </ul>
      <p v-else class="mt-3 text-center">Não há tarefas disponíveis.</p>
  </div>
</template>

<style scoped>
.concluida {
  text-decoration: line-through;
}
</style>

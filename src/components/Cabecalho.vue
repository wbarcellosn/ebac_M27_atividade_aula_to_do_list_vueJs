<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>

<template>
    <header class="p-5 my-4 bg-light rounded-3">
        <h1>Minhas Tarefas</h1>
        <template v-if="props.tarefasPendentes > 0">
            <p>Você possui {{ props.tarefasPendentes }} tarefas pendentes.</p>
        </template>
        <template v-else>
            <p>Não há tarefas pendentes no momento.</p>
        </template>
    </header>
</template>
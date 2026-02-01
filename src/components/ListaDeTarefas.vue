<script setup>
    const props = defineProps(['tarefas'])
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas"> <!-- itera sobre a lista de tarefas -->
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox"> <!-- vincula o estado da checkbox ao atributo finalizada -->
        <label :class="{ done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">
            {{tarefa.titulo}} <!-- exibe o título da tarefa -->
        </label>
        </li>
    </ul>
</template>

<style scoped>
    .done {
    text-decoration: line-through;
    }
</style>
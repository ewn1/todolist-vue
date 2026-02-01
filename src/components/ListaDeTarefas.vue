<script setup>
    const props = defineProps(['tarefas', 'filtro']) // Recebendo as tarefas filtradas e o nome do filtro do App.vue
</script>

<template>
    <div v-if="props.tarefas.length === 0" class="mt-4 text-center">
        <p v-if="props.filtro === 'finalizadas'" class="text-muted">
            Você não possui tarefas concluídas.
        </p>
        <p v-else-if="props.filtro === 'pendentes'" class="text-muted">
            Você não possui tarefas pendentes.
        </p>
        <p v-else class="text-muted">
            Sua lista de tarefas está vazia.
        </p>
    </div>

    <ul v-else class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas" :key="tarefa.titulo">
            <input 
                @change="evento => tarefa.finalizada = evento.target.checked" 
                :checked="tarefa.finalizada" 
                :id="tarefa.titulo" 
                type="checkbox"
            >
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }
</style>
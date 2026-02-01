<script setup>
    const props = defineProps(['tarefasPendentes']); // define a prop que o componente espera receber do componente pai
</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>To Do List</h1>
        <p>
            Você tem {{ props.tarefasPendentes }} tarefas pendentes. <!-- exibe o número de tarefas pendentes --> <!-- usa props para receber o valor do componente pai -->
        </p>
    </header>
</template>
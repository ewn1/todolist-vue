<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit="props.cadastraTarefa">
        <div class="row">
        <div class="col">
            <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required type="text" class="form-control" placeholder="Digite a descrição da tarefa">
        </div>
            <div class="col-md-2">
            <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
            <select @change="props.trocarFiltro" class="form-control">
                <option value="todas">Todas tarefas</option>
                <option value="pendentes">Pendentes</option>
                <option value="finalizadas">Finalizadas</option>
            </select>
            </div>
        </div>
    </form>
</template>
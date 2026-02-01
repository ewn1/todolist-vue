<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    { 
      titulo: 'Estudar ES6', 
      finalizada: false,
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false,
    },
    {
      titulo: 'Ir para a academia',
      finalizada: true,
    }
  ]
})

const getTarefasPendentes = () => { // função para obter tarefas pendentes
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => { // função para obter tarefas pendentes
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => { //função para obter tarefas filtradas
  const { filtro } = estado;

  switch(filtro) { // switch faz a verificação do filtro selecionado, vários ifs poderiam ser usados também
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = (e) => { // função para cadastrar nova tarefa
  e.preventDefault(); // previne o comportamento padrão do form (recarregar a página)
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova); // adiciona a nova tarefa na lista de tarefas
  estado.tarefaTemp = ''; // limpa o campo de entrada após cadastrar a tarefa, mas precisa incluir no input :value="estado.tarefaTemp"
}
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>To Do List</h1>
      <p>
        Você tem {{ getTarefasPendentes().length }} tarefas pendentes. <!-- exibe o número de tarefas pendentes -->
      </p>
    </header>
    <form @submit="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @input="evento => estado.tarefaTemp = evento.target.value" required type="text" class="form-control" placeholder="Digite a descrição da tarefa">
        </div>
          <div class="col-md-2">
            <button type="submit" class="btn btn-primary">Cadastrar</button>
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
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()"> <!-- itera sobre a lista de tarefas -->
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox"> <!-- vincula o estado da checkbox ao atributo finalizada -->
        <label :class="{ done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">
          {{tarefa.titulo}} <!-- exibe o título da tarefa -->
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

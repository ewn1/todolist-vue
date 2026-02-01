<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';

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
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" /> <!-- passa o número de tarefas pendentes como prop -->
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" /> <!-- passa as funções e dados necessários como props -->
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" /> <!-- passa a lista de tarefas filtradas como prop -->
  </div>
</template>
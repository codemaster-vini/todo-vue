<script setup>
  import { reactive } from 'vue';
  import Cabecalho from "./components/Cabecalho.vue";
  import Formulario from "./components/Formulario.vue";
  import ListaDeTarefas from "./components/ListaDeTarefas.vue";

  const estado = reactive({
    filtro: "todas",
    tarefaTemp: "",
    tarefas: [{
      titulo: "Estudar ES6",
      finalizado: false
    },
    {
      titulo: "Estudar SASS",
      finalizado: false
    },
    {
      titulo: "Ir para academia",
      finalizado: true
    }
  ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter((tarefa) => tarefa.finalizado === false)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter((tarefa) => tarefa.finalizado === true)
  }

  const getTarefasFiltradas = () => {
    const filtro = estado.filtro;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastrarTarefa = (evento) => {
    evento.preventDefault()

    const tarefaTemporaria = {
      titulo: estado.tarefaTemp,
      finalizado: false
    }

    estado.tarefas.push(tarefaTemporaria)
    estado.tarefaTemp = "";
  }
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastrar-tarefa="cadastrarTarefa" :trocar-filtro="evento => estado.filtro = evento.target.value"/>
    <ListaDeTarefas :tarefas-filtradas="getTarefasFiltradas()" :tarefas-pendentes="getTarefasPendentes()"/>
  </div>
</template>
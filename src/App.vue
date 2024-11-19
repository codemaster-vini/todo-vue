<script setup>
  import { reactive } from 'vue';

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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>

    <form @submit="cadastrarTarefa">
    <div class="row">
      <div class="col">
        <input v-bind:value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" class="form-control" type="text" placeholder="Digite aqui a descrição da tarefa">
      </div>
      <div class="col-md-2">
        <button class="btn btn-primary" type="submit">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="evento => estado.filtro = evento.target.value" class="form-control">
          <option value="todas">Todas as tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>

  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
      <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado" :id="tarefa.titulo" type="checkbox">
      <label :class="{ finalizada: tarefa.finalizado == true}" class="ms-3" :for="tarefa.titulo">
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
  </div>
</template>

<style scoped>
  .finalizada{
    text-decoration: line-through;
    color: lightgrey;
  }
</style>
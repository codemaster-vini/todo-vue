<script setup>
    const props = defineProps(["tarefasFiltradas", "tarefasPendentes"])
</script>

<template>
    <ul v-if="props.tarefasPendentes.length >= 1" class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefasFiltradas">
            <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ finalizada: tarefa.finalizado == true }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>

    <ul v-else class="list-group mt-4">
        <li class="list-group-item">
            Você não tem nenhuma tarefa pendente
        </li>
    </ul>
</template>

<style scoped>
  .finalizada{
    text-decoration: line-through;
    color: lightgrey;
  }
</style>
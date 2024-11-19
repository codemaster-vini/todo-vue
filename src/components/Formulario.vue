<script setup>
    const props = defineProps(["cadastrarTarefa", "tarefaTemp", 'editaTarefaTemp', "trocarFiltro"])
</script>


<template>
    <form @submit="props.cadastrarTarefa">
        <div class="row">
            <div class="col">
                <input v-bind:value="props.tarefaTemp" @change="props.editaTarefaTemp" class="form-control" type="text" placeholder="Digite aqui a descrição da tarefa">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>
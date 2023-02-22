<script setup>
    const props = defineProps(['tarefas'])
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <!--UTILIZANDO O FOR DO ARRAY DE OBJETOS, COM O ITEM TAREFAS-->
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo" type="checkbox"> <!--UTILIZAMOS O : PARA ACESSAR AS PROPRIEDADES DO JS EM HTML-->
            <label :class="{ done: tarefa.finalizada }" :for="tarefa.titulo" class="ms-3">{{ tarefa.titulo }}</label>
            <!--O FOR DESTA LINHA É REFERENTE AO LABEL, NÃO FOR DE LOOPING-->
        </li>
</ul>
</template>
<style scoped>
    .done {
        text-decoration: line-through;
    }
</style>
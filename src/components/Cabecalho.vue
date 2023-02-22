<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>
<template>
    <header class="p-5 mb-4 mt-4 bg-light roundend-3">
        <h1>Minhas tarefas</h1>
        <p>
            Você possui {{ props.tarefasPendentes }} tarefas pendentes <!--AQUI COLOCAMOS A LENGTH DAS TAREFAS QUE NÃO ESTÃO FINALIZADAS-->
        </p>
    </header>
</template>
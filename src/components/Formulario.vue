<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemporaria', 'trocarFiltro', 'editaTarefaTemporaria'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <!--O .prevent TERÁ O MESMO PAPEL DO PREVENTDEFAULT, QUE NÃO IRÁ REINICIAR O FORMULARIO-->
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemporaria" @change="props.editaTarefaTemporaria"
                    type="text" placeholder="Digite a descrição da terafa" class="form-control" required>
                <!--AQUI SERÁ RESPONSÁVEL POR RECEBER E GUARDAR O VALOR DIGITADO NO INPUT PARA O ITEM TAREFATEMPORARIA-->
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">
                    Cadastrar
                </button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
</form></template>
<script setup>
import { reactive } from 'vue';

const estado = reactive( { //ARRAY DE OBJETOS
  filtro: 'todas',
  tarefaTemporaria: '',
  tarefas: [{
    titulo: 'Estudar ES6',
    finalizada: false,
  },
  {
    titulo: 'Estudar SASS',
    finalizada: false,
  },
  {
    titulo: 'Ir para academia',
    finalizada: true,
  }
]
})

const pegarTarefasPendentes = () => {
  return estado.tarefas.filter(item => !item.finalizada) //AQUI FILTRAMOS APENAS OS ITENS QUE ESTIVEREM COM FALSE NO VALOR FINALIZADA
}

const pegarTarefasFinalizadas = () => {
  return estado.tarefas.filter(item => item.finalizada)
}

const pegarTarefasFiltradas = () => {
  const { filtro } = estado //AQUI REALIZAMOS A DESESTRUTURAÇÃO DE OBJETOS, PASSANDO O {NOME DO ITEM DO OBJETO} = NOME DO OBJETO

  switch (filtro) { //AQUI O SWITCH FUNCIONA COMO VARIOS IF E ELSES, TESTANDO CONDIÇÕES
    case 'pendentes': //AQUI CASO O VALUE DO SELECT FOR pendentes IRA RETORNAR ESSA FUNÇÃO ABAIXO
      return pegarTarefasPendentes();
    case 'finalizadas': //AQUI CASO O VALUE DO SELECT FOR finalizadas IRA RETORNAR ESSA FUNÇÃO ABAIXO
      return pegarTarefasFinalizadas();
    default: //AQUI O DEFAULT SERÁ TODAS AS TAREFAS
      return estado.tarefas
  }
}

const cadastraTarefa = () => { //AQUI É A FUNÇÃO QUE SERÁ RESPONSÁVEL POR CRIAR UM ARRAY DE OBJETO E EFETUAR O PUSH PARA O OBJETO ESTADO
  const tarefaNova = { //AQUI IRÁ TER O MESMO PADRÃO DO ITEM TAREFA DO ARRAY DE OBJETO TAREFAS
    titulo: estado.tarefaTemporaria,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova) //AQUI SERÁ O PUSH DO OBJETO TAREFA NOVA PARA O ARRAY DE OBJETOS TAREFAS DO ESTADO 
  estado.tarefaTemporaria = '' //PARA ASSIM QUE O USUARIO CLICAR EM CADASTRAR, O CAMPO DO INPUT LIMPAR 
}
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light roundend-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ pegarTarefasPendentes().length }} tarefas pendentes <!--AQUI COLOCAMOS A LENGTH DAS TAREFAS QUE NÃO ESTÃO FINALIZADAS-->
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa"> <!--O .prevent TERÁ O MESMO PAPEL DO PREVENTDEFAULT, QUE NÃO IRÁ REINICIAR O FORMULARIO-->
    <div class="row">
      <div class="col">
        <input :value="estado.tarefaTemporaria" @change="evento => estado.tarefaTemporaria = evento.target.value" type="text" placeholder="Digite a descrição da terafa" class="form-control" required> <!--AQUI SERÁ RESPONSÁVEL POR RECEBER E GUARDAR O VALOR DIGITADO NO INPUT PARA O ITEM TAREFATEMPORARIA-->
      </div>
      <div class="col-md-2">
        <button class="btn btn-primary" type="submit">
          Cadastrar
        </button>
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
    <li class="list-group-item" v-for="tarefa in pegarTarefasFiltradas()"> <!--UTILIZANDO O FOR DO ARRAY DE OBJETOS, COM O ITEM TAREFAS-->
      <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox"> <!--UTILIZAMOS O : PARA ACESSAR AS PROPRIEDADES DO JS EM HTML-->
      <label :class="{done: tarefa.finalizada}" :for="tarefa.titulo" class="ms-3">{{ tarefa.titulo }}</label> <!--O FOR DESTA LINHA É REFERENTE AO LABEL, NÃO FOR DE LOOPING-->
    </li>
  </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>

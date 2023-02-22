<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue' //ASSIM IMPORTAMOS OS ARQUIVOS .vue PARA O VUE
  import Formulario from './components/Formulario.vue'
  import ListaDeTarefas from './components/ListaDeTarefas.vue'

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
    <Cabecalho :tarefas-pendentes="pegarTarefasPendentes().length" /> <!--ASSIM CRIAMOS AS TAGS PERSONALIZADAS, IMPORTANDO VIA ARQUIVOS EXTERNOS QUE CRIAMOS NO COMPONENTS-->
    <Formulario :tarefa-temporaria="estado.tarefaTemporaria" :edita-tarefa-temporaria="evento => estado.tarefaTemporaria = evento.target.value" :cadastra-tarefa="cadastraTarefa" :trocar-filtro="evento => estado.filtro = evento.target.value"/>
    <ListaDeTarefas :tarefas="pegarTarefasFiltradas()"/>
  </div>
</template>

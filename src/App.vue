<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue'


const estado = reactive({ //modulo
  filtro:'todas',
  tarefasTemporarias:'',
  tarefas: [
    {
      titulo: 'Estudar ES6', //objetos
      finalizada: false,
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false,
    },
    {
      titulo: 'Ir ve animeee',
      finalizada: true,
    }
  ]
})
//npm run dev
  const getTarefasPendentes = () => { 
    return estado.tarefas.filter(tarefa => !tarefa.finalizada) //pegando o estado das tarefas e filtrando pra ter um return pra pegar as tarefas q tao finalizadas com false,em filter ali nos () a gente pega tarefa do v-for q criamos la em baixo q faz referencia a estado.tarefas
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada) //msm coisa da const acima mas aqui o return é pra quandoa condiçao for true
  }

  const getTarefasFiltradas = () => {//const feita pra selecionar as opçoes filtradas
    const {filtro} = estado //passando q vamos pegar apenas filtro do estado

    switch (filtro) { //switch é mudança ou seja estou fazendo uma mudança no filtro
      case 'Pendentes': 
        return getTarefasPendentes(); //case(caso) chamar por Pendentes retorna a function de condiçao false! das tarefas.finalizada
      case 'Finalizadas':
        return getTarefasFinalizadas(); //case chamar finalizadas retorna os true
      default:
        return estado.tarefas;//quando for um valor diferente dos 2 acima retorna tarefa apenas
    }
  }

  const cadastrarTarefa = () => {
    const tarefaNova = { //criando um objeto com a ms estrutura do array[]
      titulo: estado.tarefasTemporarias,
      finalizada: false,//tarefa tem q começar como pendente
    }
    estado.tarefas.push(tarefaNova )//puxando tarefaTemp pra tarefas ,o q a gente digitou la no input aramzenou na ''string vazia e é puxada para ca assim adionando a tarefas com false atraves do push
    estado.tarefasTemporarias = ''; //para dps de submit o input ficar vazio
  }

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>  <!--esse :tarefas-pendentes a gente tras do Cabecalho.vue dps de definir os props-->
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento =>estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastrarTarefa" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/> 
  
  </div>
</template>





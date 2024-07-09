<script setup>
import { reactive } from 'vue';


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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastrarTarefa"> <!--evento de submit colocado com @, o prevent para fazer o prevetdefault de formoa mais simples e assim o site n recarrega-->
    <div class="row">
      <div class="col">
        <input :value="estado.tarefasTemporarias" @change="evento => estado.tarefasTemporarias = evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control"><!--evento change(mudança) => acessa estado.tarefasTemporarias que é uma '' string vazia para poder armazenar o que escrevermos no input no inicio alvo no valor ou seja no que for digitado -->
      </div>
      <div class="col-md-1"><!--(LEMBRETE)md signica medio-->
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="evento => estado.filtro = evento.target.value" class="form-control">
          <option value="todas">Todas as tarefas</option>
          <option value="Pendentes">Pendentes</option>
          <option value="Finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4"><!--list group da aparaencia de lista-->
    <li class="list-group-item" v-for="tarefa in  getTarefasFiltradas() "><!--estou falando aqui q quando chamar por tarefa ela tras o  getTarefasFiltradas() criado no JS-->
      <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo"  type="checkbox"><!--para se tornar dinamico temos q colcoar os : ai aponta pro checked q vai ser = tarefa.finalizada assim ele tem acesso ao nosso js e ve que la finalizada ta como false e n marca a checkbox ou true q vai marcar lembra dinamica por conta dos :-->
      <!--change aplica mudança pra quando apertamos pra marcar a tarefa quando marcada T se n ta F e o evento tem alvo vai pra checked-->
      <label :class="{done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo"> <!--ms-margin start--> <!--aqui a msm coisa do comentario aqui de cima mas agr aqui com titulo e o :for vai aparecer todos os titulos e o :class q tem done é pra add uma linha pra indicar no que esta marcado -->
        {{tarefa.titulo}}<!-- tenho acesso a tarefa e é possivel chamar aqui por conta do in ali de cima q fez referencia ao JS-->
      </label>
    </li>
  </ul>
  </div>
</template>

<style scoped>

.done {
  text-decoration: line-through;
}

</style>



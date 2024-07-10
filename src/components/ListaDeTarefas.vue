<template>
    <ul class="list-group mt-4"><!--list group da aparaencia de lista-->
        <li class="list-group-item" v-for="tarefa in  getTarefasFiltradas() ">
            <!--estou falando aqui q quando chamar por tarefa ela tras o  getTarefasFiltradas() criado no JS-->
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo"
                type="checkbox"><!--para se tornar dinamico temos q colcoar os : ai aponta pro checked q vai ser = tarefa.finalizada assim ele tem acesso ao nosso js e ve que la finalizada ta como false e n marca a checkbox ou true q vai marcar lembra dinamica por conta dos :-->
            <!--change aplica mudança pra quando apertamos pra marcar a tarefa quando marcada T se n ta F e o evento tem alvo vai pra checked-->
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo"> <!--ms-margin start-->
                <!--aqui a msm coisa do comentario aqui de cima mas agr aqui com titulo e o :for vai aparecer todos os titulos e o :class q tem done é pra add uma linha pra indicar no que esta marcado -->
                {{tarefa.titulo}}<!-- tenho acesso a tarefa e é possivel chamar aqui por conta do in ali de cima q fez referencia ao JS-->
            </label>
    </li>
</ul>
</template>
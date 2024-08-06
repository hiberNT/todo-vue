<script setup>
    const props = defineProps(['tarefasPendentes']) //props é propiedades esse difineProps é uma funcao do vue para q possamos corrigir os erros quando separarmos os arquivos
</script> <!-- a gente passa um nome parecido com q esta dando erro e substitui o erro pelo o nome na array e coloca .props criado ai la no primiero arquivo p App.vue vamos recuperar esses q estavo dando erro-->
<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas tarefas</h1>
        <p>
            Você possui {{ props.tarefasPendentes }} tarefas pendentes
        </p>
    </header>
</template>


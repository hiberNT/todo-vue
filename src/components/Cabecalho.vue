<script setup>
    const props = defineProps(['tarefasPendentes']) //props é propiedades esse difineProps é uma funcao do vue para q possamos corrigir os erros quando separarmos os arquivos
</script>
<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas tarefas</h1>
        <p>
            Você possui {{ props.tarefasPendentes }} tarefas pendentes
        </p>
    </header>
</template>


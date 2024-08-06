<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>
<template>
<form @submit.prevent="props.cadastraTarefa"> <!--evento de submit colocado com @, o prevent para fazer o prevetdefault de formoa mais simples e assim o site n recarrega-->
    <div class="row">
        <div class="col">
            <input :value="props.tarefasTemporarias" @change="props.editaTarefaTemp" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control"><!--evento change(mudança) => acessa estado.tarefasTemporarias que é uma '' string vazia para poder armazenar o que escrevermos no input no inicio alvo no valor ou seja no que for digitado -->
        </div>
        <div class="col-md-1"><!--(LEMBRETE)md signica medio-->
            <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
            <select @change="props.trocarFiltro" class="form-control">
            <option value="todas">Todas as tarefas</option>
            <option value="Pendentes">Pendentes</option>
            <option value="Finalizadas">Finalizadas</option>
            </select>
        </div>
    </div>
</form>
</template>
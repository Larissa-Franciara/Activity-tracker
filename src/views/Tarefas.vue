<template>

  <Formulario @aoSalvarTarefa="salvarTarefa"/>
  <div class="lista">
    <Tarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
    <Box v-if="listaEstaVazia">
      BORA TOMAR UM COFFEE É MELHORAR ESSA PRODUTIVIDADE ? <span style="font-size: 40px;">&#9749;</span>
    </Box>
    <Tarefa v-for="(tarefa, index) in tarefas" :tarefa="tarefa" :key="index"/>
  </div>


</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Formulario from '../components/Formulario.vue'
import Tarefa from '../components/Tarefa.vue'
import ITarefa from '../interface/ITarefa'
import Box from '../components/Box.vue'


export default defineComponent({
  name: 'App',
  components: {
    Formulario,
    Tarefa,
    Box
  },
  data () {
    return {
      tarefas: [] as ITarefa[]
    }
  },
  computed: {
    listaEstaVazia (): boolean {
      return this.tarefas.length === 0
    }
  },
  methods: {
    salvarTarefa (tarefa: ITarefa): void {
      this.tarefas.push(tarefa)
    },
  }


});
</script>

<style>


</style>

<template>
<main class="class columns is-gapless is-multiline" :class="{'modo-escuro': modoEscuroAtivo}">
  <div class="column is-one-quarter">
  <BarraLateral @aoTemaAlterado="trocarTema" />
  </div>
  <div class="column is-three-quarter conteudo">
  <Formulario @aoSalvarTarefa="salvarTarefa"/>
    <div class="lista">
      <Tarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
      <Box v-if="listaEstaVazia">
        BORA TOMAR UM COFFEE É MELHORAR ESSA PRODUTIVIDADE ? <span style="font-size: 40px;">&#9749;</span>
      </Box>
    </div>
  </div>
</main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue'
import Formulario from './components/Formulario.vue'
import Tarefa from './components/Tarefa.vue'
import ITarefa from './interface/ITarefa'
import Box from './components/Box.vue'


export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    Formulario,
    Tarefa,
    Box
  },
  data () {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false
    }
  },
  computed: {
    listaEstaVazia (): boolean {
      return this.tarefas.length === 0
    }
  },
  methods: {
    salvarTarefa (tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    },
    trocarTema (modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo
    }
   }


});
</script>

<style>
.lista {
  padding: 2rem;
}
main {
  --bg-primario: #ffffff;
  --texto-primario:#000000;
}
main.modo-escuro {
  --bg-primario: #2b2d42;
  --texto-primario:#ddd;
}
.conteudo {
  background-color: var(--bg-primario) ;
}

</style>

<template>
<div class="card">
    <div class="boxn formulario">
      <div class="columns">
        <div
            class="column is-5"
            role="form"
            style="padding: 2.75rem;"
            aria-label="Formulário para criação de uma nova tarefa"
        >
          <input
              type="text"
              class="input"
              placeholder="Qual tarefa está sendo inciada ?"
              v-model="descricao"
          />
        </div>
        <div class="column is-3"
             style="padding: 2.75rem;"
        >
          <div class="select" style=" max-width: 768px;">
            <select v-model="idProjeto">
              <option value="">Selecione o projeto</option>
              <option
                  :value="projeto.id"
                  v-for="projeto in projetos"
                  :key="projeto.id"
              >
                {{ projeto.nome }}
              </option>
            </select>
          </div>
        </div>
        <div class="column">
      <Temporizador @aoTemporizadorFinalizado="finalizarTarefa" />
        </div>
      </div>
    </div>
</div>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue'
import Temporizador from './Temporizador.vue'
import {useStore} from "vuex";
import {key} from "@/store";

export default defineComponent({
  name: "Formulario",
  emits: ['aoSalvarTarefa'],
  components: {
    Temporizador
  },
  data () {
    return {
      descricao: '',
      idProjeto: ''
    }
  },
  methods: {
    finalizarTarefa (tempoDecorrido: number): void {
     this.$emit('aoSalvarTarefa', {
       duracaoEmSegundos: tempoDecorrido,
       descricao: this.descricao,
       projeto: this.projetos.find(proj => proj.id == this.idProjeto)
     })
      this.descricao = ''
    }
  },
  setup () {
    const store = useStore(key)
    return {
      projetos: computed(() => store.state.projetos)
    }
  }
})


</script>

<style scoped>
.button {
  margin-left: 8px;
}
.box {
  background-color: var(--bg-primario);
  color: var(--texto-primario);
}

</style>
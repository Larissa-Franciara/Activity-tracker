<template>
<header>
  <h1>
    <img src="../assets/logo.svg" alt="">
  </h1>
<!--  <div class="has-text-centered">-->
  <button class="button  is-rounded"
          style="background: rgb(0, 0, 1,0 )"
          @click="alterarTema"
  >
    <img src="https://img.icons8.com/ios-glyphs/30/000000/moon-symbol.png"/>

  </button>
<!--  </div>-->
  <nav class="panel mt-5">
    <ul>
      <li>
        <router-link to="/" class="link">
          <i class="fas fa-tasks"></i>
          Tarefas
        </router-link>
      </li>
      <li>
        <router-link to="/Projetos" class="link">
          <i class="fas fa-project-diagram"></i>
          Projetos
        </router-link>
      </li>
    </ul>

  </nav>
</header>
</template>

<script lang="ts">
import {defineComponent} from 'vue'
export default defineComponent({
  name: "BarraLateral",
  emits: ['aoTemaAlterado'],
  data () {
    return  {
      modoEscuroAtivo: false
    }
  },
  computed: {
    textoBotao (): string {
      return this.modoEscuroAtivo ? 'claro' : 'escuro'
    }
  },
  methods: {
    alterarTema(): void {
      this.modoEscuroAtivo = !this.modoEscuroAtivo
      this.$emit('aoTemaAlterado', this.modoEscuroAtivo)
    }
  }
})


</script>

<style scoped>
h1 {
  text-align: center;
}
strong {
  color: #f95738
}
header {
  padding: 2rem;
  background: #025891;
  width: 100%;
  height: 100vh;

}
@media only screen and (max-width: 768px) {
  header {
    padding: 2.5rem;
    height: auto;
  }
}
.painel li {
  margin: 8px 0;
}
.link {
  color: #ffffff;
}
.link:hover {
  color: #FAF0CA;
}
</style>
<script lang="ts">
import { obterCategorias } from '@/http/index';
import type ICategory  from "../interfaces/ICategory";
import CardCategoria from "@/components/CardCategoria.vue";

export default {
  data() {
    return {
      categorias: { type: Object as PropType<ICategory>}
    };
  },
  async created() {
    this.categorias = await obterCategorias();
    console.log(this.categorias)
  },

  components: { CardCategoria },
  emits: ['adicionarIngrediente']
};
</script>

<template>
  <section class="selecionar-ingredientes">
    <h1 class="cabecalho titulo-ingredientes">Ingredientes</h1>
    <p class="paragrafo-lg instrucoes">
      Selecione abaixo os ingredientes que você quer usar nesta receita:
    </p>
    <ul class="categorias">
        <li v-for="categoria in categorias" key="categoria.nome">
            <CardCategoria :categoria="categoria" key="categoria.nome" @adicionar-ingrediente="$emit('adicionarIngrediente', $event)"/>
        </li>
    </ul>
  </section>
</template>

<style scoped>

.selecionar-ingredientes {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-ingredientes {
  color: var(--verde-medio, #3D6D4A);
  display: block;
  margin-bottom: 1.5rem;
}

.instrucoes {
  margin-bottom: 2rem;
}

.categorias {
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.dica {
  align-self: flex-start;
  margin-bottom: 3.5rem;
}

@media only screen and (max-width: 767px) {
  .dica {
    margin-bottom: 2.5rem;
  }
}

</style>

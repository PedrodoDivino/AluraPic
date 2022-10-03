<template>
  <div class="corpo">
    <input
      type
      seach
      class="filtro"
      placeholder="filtre por titulo"
      @:input="filtro = $event.target.value"
    />
    <h1 class="centralizado">{{ titulo }}</h1>

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro" :key="foto.id">
        <meu-painel :titulo="foto.titulo">
          <imagem-responsiva  :url="foto.url" :titutlo="foto.titulo"/>
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from "./components/shared/painel/Painel.vue";
import ImagemResponsiva from './components/shared/imagem-responsiva/imagem-responsiva.vue';
export default {
  components: {
    "meu-painel": Painel,
    'imagem-responsiva': ImagemResponsiva
  },

  data() {
    return {
      titulo: "Alurapic",
      fotos: [],
      filtro: ""
    };
  },
  computed : {
fotosComFiltro(){
if (this.filtro){
  let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
}else{
return this.fotos;
}
}
  },

  created() {
    this.$http
      .get("http://localhost:3000/v1/fotos")
      .then(res => res.json())
      .then(
        fotos => (this.fotos = fotos),
        err => console.log(err)
      );
  }
};
</script>

<style>
.corpo {
  font-family: Helvetica, sans-serif;
  width: 96%;
  margin: 0 auto;
}

.centralizado {
  text-align: center;
}

.lista-fotos {
  list-style: none;
}

.lista-fotos .lista-fotos-item {
  display: inline-block;
}


.filtro {
  display: block;
  width: 100%;
}
</style>

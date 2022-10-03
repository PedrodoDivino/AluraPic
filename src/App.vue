<template>
  <div class="corpo">
    <h1 class="centralizado">{{ titulo }}</h1>
    <ul>
      <li class="lista-fotos" v-for="foto in fotos" :key="foto">
        <img :src="foto.url" :alt="foto.titulo" :key="foto.id" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titulo: "Alurapic",
      fotos: []
    };
  },
  created() {
    this.$http
      .get("http://localhost:3000/v1/fotos")
      .then(res => res.json())
      .then(fotos => ((this.fotos = fotos), err => console.log(err)));
  }
};
</script>
<style>
  .corpo {
    font-family: Helvetica, sans-serif;
    width: 96%;
    margin: 0 auto;

  }
  .centralizado{
    text-align: center;

  }
  .lista-fotos{
    list-style: none;
  }
  .lista-fotos{
    display: inline-block;
  }
</style>

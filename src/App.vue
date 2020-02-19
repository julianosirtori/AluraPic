<template>
<div>
  <h1>{{titulo}}</h1>
  <ul>
    <li v-for="foto of fotos" :key="foto.titulo">
      <img :src="foto.url" :alt="foto.titulo" />
    </li>
  </ul>
  
</div>
</template>

<script>
export default {
    data(){
      return {
        titulo: 'Alurapic',
        fotos: [
          {
            url: "https://abrilsuperinteressante.files.wordpress.com/2018/05/filhotes-de-cachorro-alcanc3a7am-o-c3a1pice-de-fofura-com-8-semanas1.png",
            titulo: 'cachorro'
          },
          {
            url: "https://abrilsuperinteressante.files.wordpress.com/2016/03/cachorro.png",
            titulo: 'cachorro2'
          }
        ]
      }
    }
}
</script>

<style>
</style>

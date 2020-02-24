<template>
<div>
  <h1 class="centralizado">{{titulo}}</h1>
  <input type="search" @input="filtro = $event.target.value" class="filtro" placeholder="filtre por parte do título" />
  {{filtro}}
  <ul class="lista-fotos">
    <li class="lista-fotos-item" v-for="foto of fotosComFiltro" :key="foto.titulo">
      <meu-painel :titulo="foto.titulo">
        <imagem-responsiva v-meu-transform="15" :url="foto.url" :titulo="foto.titulo" />
        <meu-botao  estilo="padrao" :confirmacao="false" tipo="button" rotulo="REMOVER" @botaoAtivado="remove(foto)" />
      </meu-painel>
    </li>
  </ul>
  
</div>
</template>

<script>
import Painel from '../shared/painel/Painel';
import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva';
import Botao from '../shared/botao/Botao.vue';

export default {

    components: {
      'meu-painel': Painel,
      'imagem-responsiva': ImagemResponsiva,
      'meu-botao': Botao
    },

    data(){
      return {
        titulo: 'Alurapic',
        fotos: [],
        filtro: ''
      }
    },

    computed:{
      fotosComFiltro(){
          if(this.filtro){
            let exp = new RegExp(this.filtro.trim(), 'i');
            return this.fotos.filter(foto => exp.test(foto.titulo));
          }else{
            return this.fotos;
          }
      }
    },

    methods: {
      remove(foto) {
          alert('Remover a foto!' + foto.titulo)
      } 
    },

    created(){
      this.$http.get('http://localhost:3000/v1/fotos')
        .then(res => res.json())
        .then(fotos => this.fotos = fotos);
    }
}
</script>

<style>

.corpo{
  font-family: Arial, Helvetica, sans-serif;
  width: 96%;
  margin: 0 auto;
}

.centralizado{
  text-align: center;
}

.lista-fotos{
  list-style: none;
}

.lista-fotos-item{
  display: inline-block;
}

.imagem-responsiva{
  width: 100%;
}

.filtro{
  display: block;
  width: 100%;
}
</style>

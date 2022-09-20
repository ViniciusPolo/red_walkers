<template>
  <div class="titulo">
    <h1>Red Walkers Ranking</h1>
    </div>
  <div>
    <a href="https://transcendent-meerkat-085b98.netlify.app" target="blank"><button class="button">Jogar</button></a>
    <button class="button" v-on:click="alfabetica()">A - Z</button>
    <button class="button" v-on:click="maiorMenor()">Maior - Menor</button>
    <button class="button" v-on:click="atualizar()">Atualizar</button>
  </div>
  <div>
    <table style="margin:80px;">
      <tr class="altura">
        <td class="largura">Nome</td>
        <td class="largura">Pontuação</td>
      </tr>
      <tr v-for="nome in ranking" :key="nome" class="altura">
        <td class="largura">
          {{nome.nome}}
        </td>
        <td class="largura">
          {{nome.pontos}}
        </td>
      </tr>
    </table>
  </div>
</template>
<script>

export default {
  data(){
    return{
      ranking : [],
    }
  },
  methods: {
    async getRanking() {
      const req = await fetch("https://redwalkers-db795-default-rtdb.firebaseio.com/ranking.json");

      const data = await req.json();
      console.log(data)

      for(const name in data){
        this.ranking.push({nome: name,
                          pontos: data[name]})

      }  
      console.log(this.ranking)

      
    },

    async alfabetica(){
      this.ranking.sort(function(a,b) {
      return a.nome > b.nome;
      });

    },

    async maiorMenor(){
      this.ranking.sort(function(a,b) {
      return a.pontos < b.pontos;
      });
    },
    
  async atualizar(){
    this.ranking = [];
    this.getRanking();
  }

  },
  mounted() {
    this.getRanking();
  }
}
</script>

<style>
  *{
    font-family: Helvetica;
    box-sizing: border-box; /*Para os elementos não passarem o elemento pai */
  }
  
  .altura{
    height: 50px;
  }

  .largura{
    width: 800px;
    background: rgb(197, 197, 197);
  }

  .button{
    height: 100px;
    position: relative;
    margin-left: auto;
    margin-right: auto;
    width: 300px;
    border: solid #a71d1d 2px;
    margin: 5px;
    background-color: #a71d1d;
    color: #ffff;
    text-decoration: none;
    cursor: pointer; 
    border-radius: 10px;
  }


</style>

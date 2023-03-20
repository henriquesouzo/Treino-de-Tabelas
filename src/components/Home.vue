<template>
  <div class="home">

    <div class="imagem">
    </div>

    <table class="tabela1">
      <caption>População das Unidades Federativas</caption> <!-- titulo da tabela que sempre fica no topo -->

      <thead>
        <tr>
          <th>Posição</th>
          <th>Estado</th>
          <th>População</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="populacao in habitantes" :key="populacao.id">
          <td>{{populacao.id}}</td>
          <td>{{populacao.Estado}}</td>
          <td>{{populacao.Populacao}}</td>
        </tr>
      </tbody>

      <tfoot>
        <tr>
          <th colspan="2">Total de População:</th>
          <td>1 000 000</td>
        </tr>
      </tfoot>
    </table>

    <table class="tabela2">
      <thead>
        <tr>
          <th>Grupo</th>
          <th>Nomes</th>
          <th colspan="3">Filmes</th>
        </tr>
      </thead>

      <tbody>
        <tr>
          <th rowspan="3">Mulheres</th>
          <td>Ana Maria Santos</td>
          <td>Alien</td>
          <td>Rambo</td>
          <td>Vingadores</td>
        </tr>

        <tr>
          <td>Beatriz Sousa</td>
          <td>Hulk</td>
          <td>Inception</td>
          <td>Batman</td>
        </tr>

        <tr>
          <td>Cláudia Melo</td>
          <td>Oblivion</td>
          <td>Matrix</td>
          <td>Big Hero</td>
        </tr>

        <tr>
          <th rowspan="3">Homens</th>
          <td>Bruno Mendonça</td>
          <td>Intocáveis</td>
          <td>Amnésia</td>
          <td>Gladiador</td>
        </tr>

        <tr>
          <td>Daniel Lourenço</td>
          <td>Wall-E</td>
          <td>Oldboy</td>
          <td>Dangal</td>
        </tr>

        <tr>
          <td>Fabiano Mota</td>
          <td>Star Wars 5</td>
          <td>Taxi Driver</td>
          <td>Toy Story</td>
        </tr>
      </tbody>
    </table>    
    
  </div>
</template>

<script>
export default {
  name: 'Home',

  data(){
    return{
      habitantes: []
    }
  },

  created(){ /* assim que carregar a pagina, vai chamar a função abaixo que esta em methods */
    this.recebeHabitantes();
  },

  methods: {
    async recebeHabitantes(){
      /* instalo o json-server com o comando  npm install json-server
      depois no package.json em scripts eu adiciono  "start": "json-server --watch banco/database.json"
      depois no terminal ou prompt comando eu rodo o comando npm run start
      assim vou simular que estou recebendo dados de uma API que tem o banco de dados */
      const req = await fetch("http://localhost:3000/habitantes"); /* faço uma requisição para esta API */

      const res = await req.json(); /* recebo esta resposta que são os dados */

      this.habitantes = res;
      console.log(res);
    }
  }
}
</script>

<style scoped>
  .imagem{
    margin: 0 auto;
    padding: 20px;
    width: 20vw;
    height: 20vh;
    background-image: url("../assets/logo.png");
    background-repeat: no-repeat; /* para não repetir a imagem que se repete por padrão */
    background-position: center center;
    background-size: 10vw auto; /* se a tela diminuir(no caso na horizontal sempre), vai ajustar de acordo com a tela a imagem */
  }

  table{
    margin: 0 auto;
    border-collapse: collapse; /* para tirar os espaços entre as tabelas que vem por padrão */
  }

  table th,
  table td{
    border: 1px solid black;
    padding: 10px;
  }

  .tabela1{
    margin-bottom: 30px;
    font-family: 'Arial Narrow', Arial, sans-serif;
    position: relative; /* vai servir para eu deixar o menu da tabela fixo */
  }

  .tabela1 caption{
    margin-bottom: 5px;
  }

  .tabela1 thead{
    background-color: #2d2d2d;
    color: white;
  }

  .tabela1 tr:nth-child(2n){
    background-color: #cecaca;
  }

  .tabela1 thead th{ /* esses comandos que vai fazer o menu da tabela fixo no topo da tela e descer conforme rola o scroll do mouse */
    position: sticky;
    top: -1px;
    background-color: #2d2d2d;
  }

  .tabela2{
    margin-top: 70px;
    margin-bottom: 30px;
  }
</style>

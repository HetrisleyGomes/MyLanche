<template>
    <div class="main-container">
        <nav>
            <button @click="mudaloja('n')">ant</button> | <button @click="mudaloja('m')">prox</button>
        </nav>
        <div>
            <div class="nomelojaeditores">
                <h1>{{ nome }}</h1>
                <p v-if="promovido">
                    Loja em Destaque!
                    <button @click="promoverloja($event)" class="promovloj">Clique aqui!</button>
                </p>
                <p v-else>
                    Que tal <strong><em>PROMOVER</em></strong> a sua loja?
                    <button @click="promoverloja($event)" class="promovloj">Clique aqui!</button>
                </p>
            </div>
            <hr>
            <div>
                <table>
                    <thead>
                        <th style="text-align:center; width: 50px">ID</th>
                        <th>Produto</th>
                        <th>Preço</th>
                        <th>Promoção?</th>
                        <th>Tipo</th>
                        <th>Igredientes</th>
                        <th>Opções</th>
                    </thead>
                    <tr v-for="produto in produtos" :key="produto.id">
                        <td style="text-align:center;">{{ produto.id }}</td>
                        <td>{{ produto.item }}</td>
                        <td>{{ produto.preco }}</td>
                        <td>{{ produto.promocao}}</td>
                        <td>{{ produto.tipo }}</td>
                        <td>
                            <ul>
                                <li v-for="(i) in produto.igredientes" :key="i.index">{{ i }}</li>
                            </ul>
                        </td>
                        <td>
                            <button @click="promover($event, produto)">promoção</button>  <br>
                            <button>remover</button>
                        </td>
                    </tr>
                </table>
                <button class="botaonovo">Adicionar novo produto</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Loja',
    data() {
        return {
            num: 1,
            nome:"",
            produtos: null,
            promovido: false,
        }
    },
    methods: {
        async getLojas(n){
        const req = await fetch(`http://localhost:3000/lojas/${n}`)
        const data = await req.json();

        this.produtos = data.produtos;
        this.nome = data.nome;
        this.promovido = data.promovido;
        },

        async promover(e, produto){
            e.preventDefault();
            var pid = produto.id - 1
            this.produtos[pid].promocao = !this.produtos[pid].promocao
            var data = {
                nome: this.nome,
                promovido: this.promovido,
                produtos: this.produtos,
            }
            const datajson = JSON.stringify(data)
            const req = await fetch(`http://localhost:3000/lojas/${this.num}`,{
          method: "PUT",
          headers: {"content-type":"application/json"},
          body: datajson
        })
            
        },

        mudaloja(l){
            if (l == 'n' && this.num > 1){
                this.num --
            } else if (l == "m" && this.num < 4){
                this.num ++
            }
            this.getLojas(this.num)
        },

        async promoverloja(e){
        e.preventDefault();
            var data = {
                nome: this.nome,
                promovido: !this.promovido,
                produtos: this.produtos,
            }
            const datajson = JSON.stringify(data)
            const req = await fetch(`http://localhost:3000/lojas/${this.num}`,{
          method: "PUT",
          headers: {"content-type":"application/json"},
          body: datajson
        })
        this.getLojas(this.num)
        }

    }, mounted() {
        this.num = 1
        this.getLojas(this.num)
    }
    
}
</script>

<style scoped>
  .nomelojaeditores{
      display: flex; justify-content: flex-end; align-items: center; margin-top: 10px;
  }
  h1{color: #fff; font-weight: bold; text-shadow: #000 3px 3px 3px; margin: auto; margin-left: 25px;}
  .nomelojaeditores p{align-self: center; margin-left: 100px;}
  .promovloj{
    box-shadow:inset 0px -3px 7px 0px #9fb4f2;
	background:linear-gradient(to bottom, #7892c2 5%, #476e9e 100%);
	background-color:#7892c2;
	border-radius:3px;
	border:1px solid #4e6096;
	display:inline-block;
	cursor:pointer;
	color:#ffffff;
	font-family:Arial;
	font-size:11px;
	padding:9px 23px;
	text-decoration:none;
	text-shadow:0px 1px 0px #283966;
  }




  table {width: 100%; border-collapse: collapse;}
  th, td{
      border-bottom: #494949 solid 1px;
      padding: 10px;
      text-align: left;
      max-width: 150px;
      min-width: 150px;
  }
  tr:nth-child(even) {background-color: #aaa;}
  tr:hover{
      background-color: #888;
  }
  td:hover{
      color: #fff;
  }


  thead {
    background-color: #494949;
    color: white;
  }
  ul{
    text-align-last: start;
    list-style: none;
    font-size: 13px;
    margin: 7px 12px;
    overflow-y:none;
  }
  hr {margin-top: 30px; margin-bottom: 30px;}

  button{
      background-color: #261bc0 ;
      width:100px;
      height:40px;
      margin: 5px;
      border-width:1px;
      color:#fcba03;
      border-color:#5551aa;
      font-weight:bold;
      border-top-left-radius:8px;
      border-top-right-radius:8px;
      border-bottom-left-radius:8px;
      border-bottom-right-radius:8px;
      text-shadow: 0px 1px 0px #5551aa;
  }
  button:hover {
  background-color: #827bff;
  color: #fff;
  }
  button.botaonovo{
      position: relative;
      width:150px;
      height:90px;
      margin: 10px;
      left: 81%;
  }
</style>
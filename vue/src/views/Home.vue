<template>
  <div class="main-container">
    <div v-if="lojaspromovidas != null">
      <div v-for="loja in lojaspromovidas" :key="loja.id" class="essalojaepromovida">
        <h2>{{ loja.nome }}</h2> 
        <div class="listaloja">
          <div class="item" v-for="produto in loja.produtos" :key="produto.id">
            <span class="nome">{{ produto.item }}</span><em v-show="produto.promocao"> Promoção!</em> <br>
            <img :src="produto.img" id="logo" alt="burger">
            <ul>
              <li v-for="(ing) in produto.igredientes" :key="ing.index">{{ ing }}</li>
            </ul>
            <span class="preco" @click="addPedido($event, produto)" v-if="produto.promocao"><del>{{(produto.preco).toFixed(2)}}</del> &rArr; {{ (produto.preco * 0.75).toFixed(2) }}</span>
            <span class="preco" @click="addPedido($event, produto)" v-else>{{ (produto.preco).toFixed(2) }}</span>
          </div>
        </div>
      </div>
      <br>
    </div>

    <div>
      <Banner />
    </div>

    <div v-for="loja in lojas" :key="loja.id">
    <h2>{{ loja.nome }}</h2>    
      <div class="listaloja">
        <div class="item" v-for="produto in loja.produtos" :key="produto.id">
          <span class="nome">{{ produto.item }}</span><em v-show="produto.promocao"> Promoção!</em>
          <img :src="produto.img" id="logo" alt="burger">
          <ul>
            <li v-for="(ing) in produto.igredientes" :key="ing.index">{{ ing }}</li>
          </ul>
          <span class="preco" @click="addPedido($event, produto)" v-if="produto.promocao"><del>{{(produto.preco).toFixed(2)}}</del> &rArr; {{ (produto.preco * 0.75).toFixed(2) }}</span>
          <span class="preco" @click="addPedido($event, produto)" v-else>{{ (produto.preco).toFixed(2) }}</span>
        </div>
      </div>
      <br>
    </div>
    

  </div>
</template>

<script>
import Banner from '../components/Banner.vue'
export default {
  name: 'Home',
  data() {
    return {
      lojas: null,
      lojaspromovidas: null,
    

    }
  },
  components: {
    Banner
  },methods: {
    async getLojas(){
      const req = await fetch('http://localhost:3000/lojas?promovido=false')
      const data = await req.json();
      const req2 = await fetch('http://localhost:3000/lojas?promovido=true')
      const data2 = await req2.json();

      this.lojas = data
      this.lojaspromovidas = data2

    },
    async addPedido(e, item){
      e.preventDefault();
      item.id = null
      var po;
      if (item.promocao){
        po = item.preco
        item.preco = item.preco * 0.75
      }

      const datajson = JSON.stringify(item)

        const req = await fetch('http://localhost:3000/pedidos',{
          method: "POST",
          headers: {"content-type":"application/json"},
          body: datajson
        })

      if (item.promocao){
        item.preco = po
      }
    }
  }, mounted() {
    this.getLojas()
  },
  
}
</script>


<style scoped>
  .listaloja{
    display: flex;
    flex-wrap: nowrap;
    padding: 3px 8px;
    min-height: 220px;
    background:linear-gradient(to right, #494949 1%, #888 50%);
    margin-bottom: 5px;
    overflow-y:hidden;
    overflow-x: hidden;
    overflow: auto;
  }
  h2 {
    color: #fff;
    text-shadow: #000 2px 2px;
    background: linear-gradient(to right, #261bc0 10%, #888 90%);
    padding: 2px 5px;
    padding-right: 20px;
    border-radius: 00% 50% 50% 0%;
    max-height: 50px;
    max-width: 270px;
    cursor: context-menu;
  }
  .item {
    display: flex;
    cursor: pointer;
    text-align-last: center;
    background-color: #ddd;
    padding: 3px;
    margin: 3px;
    min-width: 200px;
    min-height: 220px;
    max-width: 200px;
    max-height: 220px;
    flex-direction: column;
    align-items: center;
    justify-content: start;
  
  }
  .item:hover {
    border: #044caa 3px solid;
    padding: 0px;
  }

  .item .nome{
    flex-wrap: nowrap;
    text-align: justify;
    font-weight:bold;
    font-size: 14px;
    padding: 7px;
  }
  .item .preco {
    background-color: #eee;
    border: #bbb solid 2px;
    color: #00ff00;
    padding: 2px 20px;
  }
  .preco:hover{
    border: #044caa solid 2px;
    background-color: #00ff00;
    color: white;
    padding: 2px 20px;
    transition: .4s;
  }

  ul{
    text-align-last: left;
    list-style: none;
    font-size:12px;
    margin: 7px 12px;
    height: 100px;
    overflow-y:scroll;
  }
  ul::-webkit-scrollbar{
    display: none;
  }
  img {
    display: block;
    width: 50%;
    max-width: 80px;
    max-height: 80px;
    margin: 0 auto;
  }

  @keyframes exemple {
    0%  {background:linear-gradient(to right, #ff0000 50%, #ddd0)}
    14% {background:linear-gradient(to right, #f5612b 50%, #ddd0)}
    28% {background:linear-gradient(to right, #e7e700 50%, #ddd0)}
    42% {background:linear-gradient(to right, #08b808 50%, #ddd0)}
    56% {background:linear-gradient(to right, #27d6cd 50%, #ddd0)}
    70% {background:linear-gradient(to right, #0000ff 50%, #ddd0)}
    84% {background:linear-gradient(to right, #690d8d 50%, #ddd0)}
    100%{background:linear-gradient(to right, #b600b6 50%,#ddd0)}
  }

  .item em {position: relative; margin-bottom: -25px; bottom: 30px; width: 100%;
    color: white; font-size: smaller; text-align: center; border-radius: 00% 50% 50% 0%;
    background-color: #a3a3a3; padding: 3px; animation-name: exemple;
    animation-duration: 7s; animation-iteration-count: infinite;
  }
  em:hover {
    opacity: 0;
  }
  .essalojaepromovida .listaloja{
    display: flex;
    flex-wrap: nowrap;
    padding: 3px 8px;
    min-height: 230px;
    background:linear-gradient(to right, #383838 1%, #888 50%);
    margin-bottom: 5px;
    overflow-y:hidden;
    overflow-x: hidden;
    overflow: auto;
  }
  .essalojaepromovida .item {
    display: flex;
    cursor: pointer;
    text-align-last: center;
    background-color: #eee;
    border: #044caa 3px solid;
    padding: 3px;
    margin: 3px;
    min-width: 230px;
    min-height: 250px;
    max-width: 230px;
    max-height: 270px;
    flex-direction: column;
    align-items: center;
    justify-content: start;
  }
  .essalojaepromovida .item:hover{
    border: #00ff00 solid 3px;
  }
  .essalojaepromovida .item .nome{
    text-align: justify;
    font-weight:bolder;
    font-size: 15px;
    padding: 7px;
  }
  .essalojaepromovida .preco:hover{
    border: #00ff00 solid 2px;
    background-color: #eee;
    color: #044caa;
    padding: 2px 20px;
    transition: .2s;
  }

  .essalojaepromovida  h2 {
    color: #fff;
    text-shadow: #000 2px 2px;
    background: linear-gradient(to right, #fcba03 2%, #888 90%);
    font-size: 30px;
    padding: 2px 5px;
    padding-right: 20px;
    border-radius: 00% 50% 50% 0%;
    max-height: 60px;
    max-width: 500px;
    z-index: 9999;
  }


</style>
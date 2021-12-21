<template>
    <div>
        <div id="tabpf">
            <h1>Pedidos</h1>
            <span> R${{ parseFloat((precofinal)).toFixed(2) }} </span>
        </div>

        <table>
            <thead>
                <th style="width:35%">Pedido</th><th style="width:35%">Igredientes</th><th colspan="2">Preço</th>
            </thead>
            <tr v-for="pedido in pedidos" :key="pedido.id">
                <td>{{pedido.item}}</td>
                <td>
                    <ul>
                        <li v-for="(i) in pedido.igredientes" :key="i.index">{{i}}</li>
                    </ul>
                </td>
                <td style="width:20%">R${{(pedido.preco).toFixed(2)}}</td>
                <td style="width:10%"><button @click="apagarItem($event,pedido.id)">Cancelar</button></td>
            </tr>
        </table>

    <div id="bfinais">
      <button @click="fim(1)">Limpar Lista de Pedidos</button>
      <button @click="fim(2)"> Finalizar Compra </button>
    </div>
    </div>
</template>
<script>
export default {
    name: 'TabelaPedidos',
    data() {
        return {
            pedidos: null,
            precofinal : null,
        }
    },
    methods: {
        async getPedidos(){
            const req = await fetch('http://localhost:3000/pedidos');
            const data = await req.json();

            this.pedidos = data;
        },
        async precototal(){
            this.precofinal = 0
            for (let i = 0; i < this.pedidos.length; i++) {
                this.precofinal += this.pedidos[i].preco
            }

        },
        async apagarItem(e, id){
          const req = await fetch(`http://localhost:3000/pedidos/${id}`, {
              method: 'DELETE'
          });
          const data = await req.json();
          this.pedidos = data;
          this.getPedidos();
            setTimeout(() => {
            this.precototal()
            },200);
        },
        async fim(n){
            if(n == 1){
                if (confirm("Apagar Lista?")){

                } else {return null}
            } else {
                if (confirm("Finalizar compra?")){

                } else {return null}
            }
        
        for (let i = 0; i <= 10; i++){
            const req = await fetch(`http://localhost:3000/pedidos/${i+1}`, {
              method: 'DELETE'
            });
        }
        this.getPedidos();
        this.precofinal = 0;

            if(n == 2){
                window.alert("Compra realizada com sucesso!")
            }

        }
    },
    created() {
        this.getPedidos();
    }, 
    mounted() {
        setTimeout(() => {
        this.precototal()
        },200);
    },
}
</script>

<style scoped>
  table{
      width: 100%;
      border-collapse: collapse;}

  #tabpf{
    display: flex;
    align-items: center;
    justify-content: flex-end;
    padding: 5px;
    margin-left: -4px;
    margin-right: 10px;
  }
  #tabpf h1{margin: auto; margin-left: 0px; background: linear-gradient(to right, #261bc0 10%, #888 90%);; border-radius: 00% 50% 50% 0%;
  width: 300px; padding: 3px; padding-left: 8px; color: #fff; text-shadow: #000 2px 2px;
  }

  #tabpf span {
      font-weight: bold;
      color: #fcba03;
      cursor: pointer;
  }

  ul{
    text-align-last: start;
    list-style: none;
    height: 50px;
    font-size: 13px;
    margin: 7px 12px;
    overflow-y:scroll;
  }
  ul::-webkit-scrollbar{
    display: none;
  }
  th, td{
      border-bottom: #494949 solid 1px;
      padding: 10px;
      text-align: left;
  }
  tr:nth-child(even) {background-color: #aaa;}
  tr:hover{
      background-color: #777; color: #fff;
  }

  thead {
    background-color: #494949;
    color: white;
  }
  button{
      background-color: #261bc0 ;
      width:100px;
      height:50px;
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
  }

  #bfinais {
      padding: 10px;
      margin: 10px;
      display: flex;
      align-items: center;
      justify-content: flex-end;
  }
  #bfinais button {
      margin-left: 25px;
  }
</style>
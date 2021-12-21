<template>
  <div class="main-container">
    <div id="botaotroca">
      <button @click="$emit('troca')">Trocar Tipo de Usuario</button>
    </div>
    <hr>
    <div id="faleconosco">
      Você também quer anunciar no nosso site? <a href="" target="_blank">Clique aqui</a> e saiba como!
    </div>
    <hr>
    <div v-if="isClient" class="aboutinfo">
        <h1>Olá loja!</h1>
        <p>Acesse sobre nossa <a href="" target="_blank">politica de privacidade</a>, e trate bem os clientes! :)</p>
        <p>Quer receber um boost nas views da sua loja? <a href="" target="_blank">Clique aqui</a> e descubra como!</p>
    </div>
    <div v-else class="aboutinfo">
      <h1>Olá Cliente!</h1>
        <p>Aproveite os melhores momentos com <em>My-Lanches</em>!</p>
        <p>Acesse sobre nossa <a href="" target="_blank">politica de privacidade.</a></p>
        <p><a href="" target="_blank">Clique aqui</a> e descubra como ganhar descontos incriveis!</p>
    </div>
    <hr>
    <div id="logo_url">
        <img src="/img/logo.png" alt="logo" id="logo">
        <span id="titulo">My-Lanche</span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      
    }
  },
  props: {isClient:Boolean}

}
</script>

<style scoped>
  #botaotroca{
    display: flex;
  }
  .aboutinfo{
    padding: 5px;
    margin: 15px;
    text-align: center;
  }

  #faleconosco{
    text-align: center;
    padding: 10px;
  }

  button{
      background-color: rgb(38, 27, 192) ;
      font-size: 25px;
      width:300px;
      height:80px;
      border-width:1px;
      color:#fcba03;
      border-color:#5551aa;
      font-weight:bold;
      margin: 0 auto;
      border-top-left-radius:8px;
      border-top-right-radius:8px;
      border-bottom-left-radius:8px;
      border-bottom-right-radius:8px;
      text-shadow: 0px 1px 0px #5551aa;

  }
  button:hover {
  background-color: #827bff;
  }
  hr {
    margin-bottom: 30px; margin-top: 20px;
  }

  #logo_url{margin: 0 auto; margin-bottom: 20px; display: flex;flex-direction: column;  
  align-items: center; border-radius: 40px; width: 280px; padding: 20px; cursor: context-menu;}
  #logo{width: 140px; height: 140px;}
  #titulo{font-weight: bold; color: #fff; font-size: 40px;}
  a {
    color: darkblue;
    text-decoration: none;
  }
</style>
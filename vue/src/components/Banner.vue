<template>
  <div id="main-burger">
      <p>Aproveite os melhores momentos com <em>My-Lanches!</em></p>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Banner'
}
</script>

<style scoped>
    #main-burger{
        background-image: url('/img/burger.jpg');
        background-position: 0 -270px;
        background-size: cover;
        height: 450px;
        display: flex;
        align-items: flex-end;
        justify-content: flex-start;
        margin: 10px 0px;
        box-shadow: #000 2px 2px 1px;
    }
    #main-burger p{
        color: #fff;
        text-align: left;
        font-size: 30px;
        background: linear-gradient(to right, #261bc0 30%, #88888800 99%);
        border-radius: 00% 50% 50% 0%;
        text-shadow: #261bc0 2px 2px 2px;
        min-width: 1200px;
        padding: 20px 40px;
        margin-bottom: 20px;
        cursor: context-menu;
    }
</style>

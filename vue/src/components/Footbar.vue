<template>
    <div id="footer">
        <p>My-Lanche &copy;</p>
        <sub>Aproveite os melhores momentos com <em>My-Lanches</em>!</sub>
        <table>
            <tr>
                <td>Entre em contato:</td><td><a href="MyLancheOficial@gmail.com" target="blank"> Teste@gmail.com</a></td>   
            </tr>
            <tr><td>Facebook:</td> <td>MyLanche</td></tr>
            <tr><td>Instagram: </td> <td>MyLanche</td></tr>
        </table>
        <p>  </p>
        <p></p>
        <p></p>


    </div>
</template>

<script>
export default {
    name: 'Footbar'
}
</script>

<style scoped>
    #footer {
    height: 200px;
    background-color: #261bc0;
    border-top: 4px solid #2b0070;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    flex-wrap: wrap;
    bottom: 0;
    width: 100%;
    cursor: context-menu;
  }
  #footer a {
      text-decoration: none;
      color: #fff;
  }
  #footer table{
      margin-top: 3px;
      font-size: small;
      text-align: initial;
  }
</style>
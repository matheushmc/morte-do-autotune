<script setup>
import { ref } from 'vue'

const btnCarrinho = ref(false)

const produtos = ref([
    {
        id: 1,
        nome: 'Camiseta',
        quantidade: 0,
        preco: 49.90
    },
    {
        id: 2,
        nome: 'Calça',
        quantidade: 0,
        preco: 99.90
    },
    {
        id: 3,
        nome: 'Meia',
        preco: 9.90,
        quantidade: 0
    },
    {
        id: 4,
        nome: 'Sapato',
        quantidade: 0,
        preco: 199.90
    },
    {
        id: 5,
        nome: 'Boné',
        preco: 29.90,
        quantidade: 0
    },
    {
        id: 6,
        nome: 'Óculos',
        quantidade: 0,
        preco: 99.90
    },
    {
        id: 7,
        nome: 'Relógio',
        quantidade: 0,
        preco: 299.90
    },
    {
        id: 8,
        nome: 'Bermuda',
        quantidade: 0,
        preco: 79.90
    },
    {
        id: 9,
        nome: 'Cueca',
        quantidade: 0,
        preco: 19.90
    },
    {
        id: 10,
        nome: 'Meia',
        preco: 9.90,
        quantidade: 0
    }
]
)
const carrinho = ref({
  items: [],
  total: 0
})

let valorTotal = ref(0)

function addcar(produto) {
  carrinho.value.items.push({
    id: produto.id, 
    nome: produto.nome, 
    preco: produto.preco, 
    quantidade: produto.quantidade,
    total: produto.preco * produto.quantidade
  });
  carrinho.value.total += produto.preco * produto.quantidade
}
function add(index){
  produtos.value[index].quantidade++
  const pos = carrinho.value.items.indexOf(carrinho.value.items.find(c => c.id===produtos.value[index].id))
  if(pos != -1) {
    carrinho.value.total -= carrinho.value.items[pos].total
    carrinho.value.items[pos].total = ++carrinho.value.items[pos].quantidade * carrinho.value.items[pos].preco 
    carrinho.value.total += carrinho.value.items[pos].total
 
  }
}
function diminui(index){
  produtos.value[index].quantidade--
}
</script>

<template>

        <div class="row"></div>

<div class="barracima">

  

    <div>
        <h1>Mercado</h1>
    </div>

   

</div>
 <div class="separa">

<div  v-for="(produto, index) in produtos" :key="produto.id">

    <div  class="corpo"> 
        <b> {{ produto.id }} - {{ produto.nome }} </b>
            <br>
        <h6>Preço: {{ produto.preco }}</h6>
        <h6>Quantidade: {{ produto.quantidade }}</h6>

        <button type="button" @click="diminui(index)" class="botao mudarcor2">-</button>
        <button type="button" @click="add(index)" class="botao mudarcor">+</button>
        <button type="button" @click="addcar(produto)" class="botao mudarcor">Adicionar</button>
  </div>

</div>
</div>

<!-- Div carrinho -->

<button type="button" class="btnCarrinho" @click="btnCarrinho = !btnCarrinho" >Carrinho</button>

<div v-if="btnCarrinho">

<!-- div v-for do carrinho -->
<div v-for="(itemCarrinho, id) in carrinho.items" :key="itemCarrinho.id" class="textCarrinho">

  <h4>{{itemCarrinho.id }} - {{ itemCarrinho.nome }} </h4>
  <p>Preço: {{itemCarrinho.preco}}</p>
  <p>Quant: {{ itemCarrinho.quantidade }}</p>
  <p>Valor total da produto: {{itemCarrinho.total }}</p>
  <hr>
  
</div>


</div>

</template>

<style scoped>



.barracima {
    display: grid;
    grid-template-columns: 100px 250px 100px;
    justify-content: space-between;
    border-bottom: rgb(0, 247, 255) solid 10px;
    font-family: 'Caveat', cursive;
}

.pidao {
    border-radius: 100px;
}

.corpo {
    font-size: 25px;
    padding: 25px;
    color: rgb(0, 0, 0);
    border: solid 10px rgb(0, 238, 255);
    border-radius: 15px;
    width: 200px;
    margin-top: 30px;
    font-family: 'Caveat', cursive;
  }

.botao {
    font-size: 25px;
    font-family: 'Caveat', cursive;
}

  .mudarcor:hover {
    transition: 0.5s;
    color: green;
  }

  .mudarcor2:hover {
    transition: 0.5s;
    color: rgb(255, 0, 0);
  }

  .imgs {
    width: 50px;
  }

  .separa{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }

  .btnCarrinho{
    color: rgb(0, 0, 0);
    padding: 30px;
    font-size: x-large;
    background-color: cyan;
    border-radius: 5px;
    margin-left: 5px;
    margin-top: 5px;
  }
  .textCarrinho{
    color: black;
    padding: 10px;
    background-color: cyan;
    width: 7%;
    border: black;
    border-radius: 5px;
    margin-left:5px ;
    margin-top: 10px;
  }
</style>

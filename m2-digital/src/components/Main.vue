<template>

    <div class="div-main">
        <p class="shopping-cart" @click.prevent="showShopCart('.div-shopping-cart')"> 🛒 </p>
        <div class="div-shopping-cart">
            <h2>Carrinho de Compras</h2>

            <div class="produto-carrinho">
                <p>Pacote de Internet: {{shopCart.internet}}</p>
                <p>Valor: R$ {{shopCart.precoInternet}}</p>
                <button @click.prevent="removeInternet">&#10060;</button>
            </div>

            <div class="produto-carrinho">
                <p>Pacote de Telefone: {{shopCart.telefone}}</p>
                <p>Valor: R$ {{shopCart.precoTelefone}}</p>
                <button @click.prevent="removePhone">&#10060;</button>
            </div>

            <div class="produto-carrinho">
                <p>Pacote de Internet: {{shopCart.planoTv}}</p>
                <p>Valor: R$ {{shopCart.precoTv}}</p>
                <button @click.prevent="removeTV">&#10060;</button>
            </div>

            <p class="valor-total">Valor total: R$ {{shopCart.precoInternet + shopCart.precoTelefone + shopCart.precoTv}}</p>
        </div>
        <div class="lista-planos">
        <h3>Selecione a opção desejada: </h3>
        <div class="button-list">
            <button @click="hideOrShowDiv('.internet', '#phone', '.tv')"> INTERNET </button>
            <button @click="hideOrShowDiv('#phone', '.tv', '.internet')"> TELEFONE </button>
            <button @click="hideOrShowDiv('.tv', '#phone', '.internet')"> TV </button>
        </div>
        </div>

        <div class="internet">
        <h2>Pacotes de Internet: </h2>
        <p> Selecione um plano de internet para continuar</p>
        <div id="div-product-internet">
            <section v-for=" (item, indice) in content" v-bind:key="indice">
                <div class="div-content" v-if="item.title == 'internet'">
                    <h2 class="h2-product">{{item.type}}</h2>
                    <p class="p-product">$ {{item.preco}}</p>
                    <button class="adc-carrinho" id="carrinho-internet" @click.prevent="addShopcartInternet(item.type, item.preco); selectTvandPhone('#phone', '.tv') "> <a href="#div-product-fixo"> Adicionar ao carrinho </a></button>
                </div>
            </section>
        </div>
        </div>

        <div class="phone" id="phone">
            <h2> Telefonia fixa: </h2>
            <p>Escolha seu pacote de telefonia fixa.</p>
            <div id="div-product-fixo">
                <section v-for=" (item, indice) in content" v-bind:key="indice">
                    <div class="div-content" v-if="item.title == 'fixo'">
                        <h2 class="h2-product" id="h2-product">{{item.type}}</h2>
                        <p class="p-product">$ {{item.preco}}</p>
                        <button class="adc-carrinho" id="carrinho-telefone" @click.prevent="addShopcartTelefone(item.type, item.preco)"> Adicionar ao carrinho </button>
                    </div>
                </section>
            </div>
        </div>

            <div class="tv">
            <h2>Pacotes de Televisão: </h2>
            <p>Agora, escolha o seu plano de TV.</p>
            <div id="div-product-tv">
                <section v-for=" (item, indice) in content" v-bind:key="indice">
                    <div class="div-content" v-if="item.title == 'tv'">
                        <h2 class="h2-product" id="h2-product-tv">{{item.type}}</h2>
                        <p class="p-product">$ {{item.preco}}</p>
                        <button class="adc-carrinho" id="carrinho-tv" @click.prevent="addShopcartTV(item.type, item.preco)"> Adicionar ao carrinho </button>
                    </div>
                </section>
            </div>
            </div>
    </div>

</template>

<script>
import axios, { Axios } from "axios";


export default {
    data(){
        return {
            'name': 'Main',
            'content': [],
            'shopCart': 
                {
                    'internet': '',
                    'precoInternet': 0,
                    'telefone': '',
                    'precoTelefone': 0,
                    'planoTv': '',
                    'precoTv': 0,
                }
            }
    },

        methods: {

        hideOrShowDiv(param1, param2, param3){
          const showDiv = document.querySelector(param1)
          const hideDiv1 = document.querySelector(param2)
          const hideDiv2 = document.querySelector(param3)

          showDiv.style.display = 'inline-block'
          if (hideDiv1.style.display != 'none' || hideDiv2.style.display != 'none'){
              hideDiv1.style.display = 'none';
              hideDiv2.style.display = 'none';
          }

        },

        selectTvandPhone(param1, param2){
            const showDiv = document.querySelector(param1);
            const showDiv2 = document.querySelector(param2);
            showDiv.style.display = 'inline-block';
            showDiv2.style.display = 'inline-block';

        },

        addShopcartInternet(type, price){
            if (this.shopCart.precoInternet == 0){
                this.shopCart.internet = type;
                this.shopCart.precoInternet = price
            } else {
                alert('Produto já adicionado ao carrinho')
                }

            
        },

        addShopcartTelefone(type, price){
            if(this.shopCart.precoTelefone == 0){
                this.shopCart.telefone = type;
                this.shopCart.precoTelefone = price;
            } else{
                alert('Produto já adicionado ao carrinho')
            }
        },

        addShopcartTV(type, price){
            if (this.shopCart.precoTv == 0){
            this.shopCart.planoTv = type;
            this.shopCart.precoTv = price;
            } else {
                alert('Produto já adicionado ao carrinho')
            }
        },

        showShopCart(param1){
            const shopCart = document.querySelector(param1)
            if (shopCart.style.display == 'none'){
                shopCart.style.display = 'inline-block'
            } else {
                shopCart.style.display = 'none'
            }
        },

        removeInternet (){
            this.shopCart.internet = ''
            this.shopCart.precoInternet = 0
        },

        removePhone (){
            this.shopCart.telefone = ''
            this.shopCart.precoTelefone = 0
        },

        removeTV (){
            this.shopCart.planoTv = ''
            this.shopCart.precoTv = 0
        },

    },

    mounted (){
        axios
            .get("http://my-json-server.typicode.com/felipecro28/m2/posts")
            .then((res) => {this.content = res.data})
            .catch((error) => {
                alert('Problema na importação da API. Tente novamente mais tarde!')
            })
        
    }
}
</script>



<style scoped>
    .div-main{              
        height: fit-content;
        background-color: #003049;
    }

    .shopping-cart{
        position: fixed;
        top: 0;
        right: 0;
        font-size: 30px;
        cursor: pointer;
        z-index: 1;

    }

    .div-shopping-cart h2{
        color: #669BBC;
        margin: 32px 0 0 0;
    }

    .div-shopping-cart{
        height: 100vh;
        width: 100%;
        background-color: #002f49fa;
        border: 2px solid #669BBC;
        position: fixed;
        top: 0;
        right: 0;
        text-align: center;
        display: none;
    }

    .produto-carrinho{
        border-bottom: 2px #669BBC solid;
        width: 70%;
        margin: 0 auto;
        padding: 30px 0;
    }

    .produto-carrinho p{
        text-transform: uppercase;
        padding-bottom: 15px;
        color: #669BBC;
    }

    .valor-total{
        color: #669BBC;
        margin: 20px 0;
        font-size: 22px;
    }


    .lista-planos{
        width: 100%;
        height: fit-content;
        background-color: #003049;
        text-align: center;
        color: #669BBC;
        border-bottom: 3px #669BBC solid;
        border-top: 3px #669BBC solid;
        border-radius: 1px;
    }

    .lista-planos h3{
        padding: 20px 0 40px 0;
        text-transform: uppercase;
        
    }

    .button-list{
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        padding-bottom: 30px;
        color: #669BBC;
    }

    button{
        color: #669BBC
    }

    .button-list button{
        width: 100px;
        height: 45px;
        background-color: #003049;
        border-radius: 5px;
        cursor: pointer;
        box-shadow: #669BBC;
        color: #669BBC;

        }

        a{
            text-decoration: none;
            color: #669BBC;
        }

    .internet{
        text-align: center;
        height: fit-content;
        width: 100%;
        background-color: #003049;
        color: #669BBC;
    }

    .internet h2{
        text-transform: uppercase;
        padding: 30px 10px 0 0;
    }

    .internet p{
        padding-bottom: 10px;
    }

    .div-content{
        height: 200px;
        width: 200px;
        border: solid 3px #669BBC;
        margin: 20px auto;
        cursor: pointer;
    }

    .tv{
        text-align: center;
        height: fit-content;
        width: 100%;
        background-color: #003049;
        color: #669BBC;
        display: none;
    }

    .tv h2{
        text-transform: uppercase;
        padding: 30px 10px 0 0;
    }

    .tv p{
        padding-bottom: 10px;
    }

    .phone{
        text-align: center;
        height: fit-content;
        width: 100%;
        background-color: #003049;
        color: #669BBC;
        display: none;
    }

    .phone h2{
        text-transform: uppercase;
        padding: 30px 10px 0 0;
    }

    .phone p{
        padding-bottom: 10px;
    }

    .div-content h2{
        padding: 10px 0;
        font-size: 27px;
    }

    .div-content p{
        padding: 10px 0 30px 0;
        font-size: 35px;
    }

    #h2-product{
        font-size: 20px;
    }


    .adc-carrinho{
        width: 80%;
        height: 35px;
        background-color: #003049;
        border-radius: 5px;
        cursor: pointer;
        box-shadow: 2px -1px #669BBC;

    }




     @media (min-width: 500px){


         .shopping-cart{
             font-size: 40px;
         }

         .div-shopping-cart{
             width: 30%;
             background-color: #002f49fa;
         }

        .div-shopping-cart h2{
            margin-top: 25px
        }
        
        .button-list button{
            width: 150px;
            height: 65px;
            font-size: 24px;
            }

        #div-product-fixo{
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            justify-content: center;
            border-bottom: 3px #669BBC solid;
        }

        #div-product-internet{
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            justify-content: center;
            border-bottom: 3px #669BBC solid;
        }

        #div-product-tv{
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            justify-content: center;
            border-bottom: 3px #333533 solid;
        }

        .div-content{
            margin: 30px 120px;

        }

    }
     




</style>
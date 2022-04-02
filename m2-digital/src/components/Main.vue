<template>
    <div class="div-main">
        <h2> Bem vindo ao nosso canal de assinaturas. </h2>
        <p> Escolha o pacote desejado</p>

        <div id="div-product-fixo">
            <section v-for=" (item, indice) in content" v-bind:key="indice">
                <div class="div-content" v-if="item.title == 'fixo'">
                    {{item.title}}
                </div>
            </section>
        </div>

        <div id="div-product-tv">
            <section v-for=" (item, indice) in content" v-bind:key="indice">
                <div class="div-content" v-if="item.title == 'tv'">
                    {{item.title}}
                </div>
            </section>
        </div>
        
        <div id="div-product-internet">
            <section v-for=" (item, indice) in content" v-bind:key="indice">
                <div class="div-content" v-if="item.title == 'internet'">
                    {{item.title}}
                </div>
            </section>
        </div>
    </div>
</template>

<script>
import axios, { Axios } from "axios";

export default {
    data(){
        return {
            'name': 'Main',
            'content': []
        }
    },

    mounted (){
        axios
            .get("http://my-json-server.typicode.com/felipecro28/m2/posts")
            .then((res) => {this.content = res.data})
            .catch((error) => {
                alert('Problema na importação da API. Tente novamente mais tarde!')
            })
        console.log(this.content)
    }
}
</script>



<style>
    .div-main{
        width: 100%;
        height: 70vh;
        background-color: rgba(103, 74, 74, 0.631);
    }

    #div-product-fixo{
        display: flex;
        width: fit-content;
        flex-direction: row;
        flex-wrap: wrap;
        margin: 0 auto;
    }

    #div-product-internet{
        display: flex;
        width: fit-content;
        flex-direction: row;
        flex-wrap: wrap;
        margin: 0 auto;
    }

    #div-product-tv{
        display: flex;
        width: fit-content;
        flex-direction: row;
        flex-wrap: wrap;
        margin: 0 auto;
    }

    .div-content{
        width: 250px;
        height: 250px;
        background-color: rgb(125, 104, 104);
        border: 2px solid grey;
        margin: 60px 55px 65px 0;
    }
</style>
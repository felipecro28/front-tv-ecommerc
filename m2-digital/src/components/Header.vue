<template>
    <div class="header-div">
     <img src="../assets/front-tv.gif" alt="logo-front">
     <p class="phone">0800-0800-0800</p>
     <p class="header-txt">Front-Tv: </p>
     <p class="header-txt" id="header-last-line">O seu plano digital de assinaturas!</p>
    </div>

    
</template>




<script>

export default {
    data(){
        return {
            'name': 'Header',
        }
    },
}
</script>


<style scoped>
    .header-div{
        width: 100%;
        height: fit-content;
        background-color: #C1121F;
        text-align: center;
        color: #FDF0D5;
        padding-bottom: 60px;
    }

    img{
        width: 180px;
        height: 180px;
        margin: 0 auto;
    }

    .phone{
        position: absolute;
        top: 0;
        left: 0;
        margin: 10px 0 0 10px;
        font-size: 12px;
    }

    #header-last-line{
            margin-top: 30px
        }

    @media (min-width: 500px){
        img{
            display: flex;
            width: 230px;
            height: 230px;
        }

        .phone{
            font-weight: bold;
            font-size: 40px;
        }

        .header-txt{
            font-size: 22px ;
        }
}


</style>

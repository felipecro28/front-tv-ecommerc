<template>
    <div class="header-div">
        <h1> TV FRONT </h1>
        <p>&#128722</p>

    </div>

    
</template>




<script>
export default {
    data(){
        return {
            'name': 'Header'
        }
    }
}
</script>


<style>
    .header-div{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        width: 100%;
        height: 10vh;
        background-color: rgba(182, 84, 35, 0.594);
        padding: 30px 70px;
    }

    h1{
        font-size: 75px;
        padding: 40px 0 0;
        color: rgb(15, 13, 13);
    }

    p{
        font-size: 90px;
    }

</style>

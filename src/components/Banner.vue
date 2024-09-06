<template>
    <div id="main-banner">
        <h1>Make Your Potion</h1>
    </div>
</template>

<script>
export default {
    name: "BanneR"

}
</script>

<style scoped>
    #main-banner{
        background-image: url('/public/img/potionw.jpeg');
        background-position: center;
        background-size: cover;
        height: 50vh;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }

    #main-banner h1 {
        color: #fff;
        text-align: center;
        font-size: 60px;
        background-color: #222;
        padding: 20px 40px;
        border: solid #fff 2px;
        border-radius: 10px;
    }

</style>
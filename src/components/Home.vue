<template>
    <div class='container'>
        <div class='row' id='home-presentation'>
            <h1>REJOIGNEZ L'EXPLORATION DE L'INGÉNIERIE POSITIVE
            </h1>

            <h3>LA CLAVETTE EN QUELQUES MOTS</h3>
                    <p><br>
            <b>POURQUOI ?</b><br>
            On considère souvent que l'ingénierie est essentiellement au service de la rentabilité économique. Or il existe une Ingénierie Positive plus humaine qu'on connaît peu et dont on ne parle pas assez.
            <br><br>
            <b>COMMENT ?</b><br>
            En montrant des exemples inspirants d’Ingénierie responsable, innovante et sociale.
            <br><br>
            <b>QUOI ?</b><br>
            Des vidéos et des articles qui présentent et expliquent des initiatives positives à travers le monde.</p>
        </div>
        <div id='home-div-button'>
            <button class='btn btn-primary' @click='beginTest'>Faire le test</button>
        </div>
    </div>
    
</template>

<script>
    export default{
        methods:{
            beginTest(){
            this.$emit('beginTest');
            }
        }
    }
</script>

<style>

#home-div-button{
    text-align:center;
    margin-top:5%;
}
</style>
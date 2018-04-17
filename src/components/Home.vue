<template>
    <div class='container' id='home-container'>
       

            <h1>Quel type d'Ingénieur Positif êtes-vous ?
            </h1>
             <div class='row' >
                 <div class='col-sm-3'></div>
            <div class='col-sm-6' id='home-description'>
                <p>Nous souhaitons tous améliorer notre monde, mais chacun à notre façon. </p><p>
                Découvrez les 6 profils qu'on rencontre le plus souvent en Ingénierie Positive.
                Rassurez-vous, pas besoin d'être ingénieur pour mettre la technologie au service de la société. </p><p>
                Une manière ludique d'en apprendre plus sur vos moyens d'action.</p>
                <h4>Prêt à connaître votre profil ?</h4> 
            </div>
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
#home-container{
    text-align:center;
}
#home-div-button{
    text-align:center;
    margin-top:2rem;
}

#home-div-button .btn-primary{
    background-color : white;
    color:rgb(83, 83, 83);;
    border:none;
    font-weight:bold;
    border-top : 0.2em solid  white;
    border-bottom : 0.3em solid  rgb(134, 206, 0) ;
    border-radius:0;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.5);
    transition: color 0.15s ease-in-out,border-color 0.3s ease-in-out;
}

#home-div-button .btn-primary:hover{
    border-bottom : 0.3em solid #5e5e5e;

}

#home-description{
    margin-top:2rem;
    background: linear-gradient(to bottom right, #0D47A1,rgb(6, 32, 71));
    padding :3rem;
}

#home-description p{
    font-size:1.2em;
    text-align: justify;
}

#home-description h4{
    font-size:1.2em;
    font-weight:bolder;
}
</style>
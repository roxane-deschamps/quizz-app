<template>
    <div class='container' id='results'>
        <div class='row'>
            <div class="col col-sm-5 col-graph">
                <h4>Bravo, vous êtes un {{profilLabels[indexMaxScore]}} !</h4>
                <canvas id="spider-chart"></canvas>
                <div id='div-retry' class="no-xs">
                    <button class='btn btn-primary'  @click='retry'>Recommencer</button>
                </div>            
            </div>
            <div class="col col-sm-7 col-explanations">
                <div class='container-fluid'>
                    <div class='row'>
                        <div class='col col-sm-9' id='results-explanations'>
                            <div class="tab-content" id="v-pills-tabContent">
                            <div class="tab-pane fade" :class="{show : this.indexMaxScore === 0, active: this.indexMaxScore === 0}" id="v-pills-alerteur" role="tabpanel" aria-labelledby="v-pills-alerteur-tab">
                                <h3>L'alerteur 
                                    <img class="long" src="../assets/img-profils/Alerteur.jpg">
                                </h3>

                                <h4>Caractéristiques</h4>
                                <p>Vous n’aimez pas les hypocrites et n’hésitez pas à donner votre avis. En soirée vous pouvez débattre des heures de sujets de société. Vous pensez que nous devons secouer les organisations car le changement, c’est maintenant !</p>
                                <h4>Super compétence</h4>
                                <p>Agiter les consciences.</p>
                                <h4>Pistes d'action</h4>
                                <ul>
                                    <li>Organiser et prendre part aux débats citoyens sur l’utilisation de la technologie.</li>
                                    <li>Créer des médias d’information autour des enjeux actuels.</li>
                                    <li>Concevoir ses produits de manière transparente.</li>
                                    <li>Dénoncer les opérations de greenwashing.</li>
                                </ul>
                            </div>
                            <div class="tab-pane fade" :class="{show : this.indexMaxScore === 1, active: this.indexMaxScore === 1}" id="v-pills-bricoleur" role="tabpanel" aria-labelledby="v-pills-bricoleur-tab">
                                <h3>Le bricoleur
                                    <img class="long" src="../assets/img-profils/Bricoleur.jpg">
                                </h3>
                                <h4>Caractéristiques</h4>
                                <p>Vous êtes passionné par la conception de systèmes. Vos amis ont l’impression que vous êtes toujours en train de bricoler. Parler c’est bien mais ce qui vous intéresse c’est de mettre la main dans le cambouis et de concrétiser les idées.</p>
                                <h4>Super compétence</h4>
                                <p>Inventer et fabriquer des solutions.</p>
                                <h4>Pistes d'action</h4>
                                <ul>
                                    <li>Rejoindre un fablab/hacklab/biolab.</li>
                                    <li>Concevoir des produits low-tech.</li>
                                    <li>Réfléchir à des solutions modulaires et libres.</li>
                                    <li>Organiser des ateliers de réparation.</li>
                                </ul>
                            </div>
                            <div class="tab-pane fade" :class="{show : this.indexMaxScore === 2, active: this.indexMaxScore === 2}" id="v-pills-collaborateur" role="tabpanel" aria-labelledby="v-pills-collaborateur-tab">
                                <h3>Le collaborateur
                                    <img class="long" src="../assets/img-profils/Collaborateur.jpg">
                                </h3>
                                <h4>Caractéristiques</h4>
                                <p>Vous adorez travailler en équipe. Pour vous seul on va peut être plus vite mais à plusieurs on va plus loin. Votre ingéniosité est multipliée quand vous réfléchissez à plusieurs et il vous parait dommage de garder une idée pour soi surtout quand elle a un impact social positif.</p>
                                <h4>Super compétence</h4>
                                <p>Travailler en équipe et communiquer.</p>
                                <h4>Pistes d'action</h4>
                                <ul>
                                    <li>Découvrir l’open source et le crowdsourcing.</li>
                                    <li>Travailler avec des méthodes d’intelligence collective.</li>
                                    <li>Rejoindre un fablab/hacklab/biolab.</li>
                                    <li>Créer des produits modulaires.</li>
                                    <li>Aller à la rencontre d’associations ou d’entreprises de l’ESS.</li>
                                </ul>
                            </div>
                            <div class="tab-pane fade" :class="{show : this.indexMaxScore === 3, active: this.indexMaxScore === 3}" id="v-pills-ecolo" role="tabpanel" aria-labelledby="v-pills-ecolo-tab">
                                <h3>L'écolo</h3>
                                 <img class="long" src="../assets/img-profils/Ecolo.jpg">
                                <h4>Caractéristiques</h4>
                                <p>Vous voyez plus loin que le bout de votre nez et la consommation de nos ressources vous inquiète. Vous ne supportez pas qu’on saccage mère Nature. Et vous pensez que la technologie doit se développer dans le respect de la planète et de ses habitants.</p>
                                <h4>Super compétence</h4>
                                <p>Voir les problèmes de façon holistique.</p>
                                <h4>Pistes d'action</h4>
                                <ul>
                                    <li>Découvrir l’économie circulaire et les low-tech.</li>
                                    <li>Faire de l’upcycling.</li>
                                    <li>Penser à la réparabilité et modularité de ses produits.</li>
                                    <li>Dénoncer l’obsolescence programmée.</li>
                                </ul>
                            </div>
                            <div class="tab-pane fade" :class="{show : this.indexMaxScore === 4, active: this.indexMaxScore === 4}" id="v-pills-humaniste" role="tabpanel" aria-labelledby="v-pills-humaniste-tab">
                                <h3>L'humaniste
                                    <img class="long" src="../assets/img-profils/Humaniste.jpg">
                                </h3>
                                <h4>Caractéristiques</h4>
                                <p>Pour vous la technologie doit être au service de l’humanité et un moyen de réduire les inégalités. Vous êtes sensible aux projets qui aident les populations défavorisées car vous pensez que les Hommes sont égaux, peu importent leur sexe, origine ou handicap.</p>
                                <h4>Super compétence</h4>
                                <p>Avoir une grande empathie.</p>
                                <h4>Pistes d'action</h4>
                                <ul>
                                    <li>Découvrir l’<i>human centered design</i> et l’innovation frugale.</li>
                                    <li>Améliorer le bien être de vos coéquipiers.</li>
                                    <li>Aller à la rencontre d’associations ou d’entreprises de l’ESS.</li>
                                    <li>Concevoir des produits qui soient inclusifs.</li>
                                </ul>
                            </div>
                            <div class="tab-pane fade" :class="{show : this.indexMaxScore === 5, active: this.indexMaxScore === 5}" id="v-pills-pedagogue" role="tabpanel" aria-labelledby="v-pills-pedagogue-tab">
                                <h3>Le pédagogue
                                    <img class="long" src="../assets/img-profils/Pedagogue.jpg">
                                </h3>
                                <h4>Caractéristiques</h4>
                                <p>Vous adorez partager vos savoirs. Vous pensez que la science est un bien commun que nous devons partager. Un petit côté Jamy de "C’est pas sorcier" mais ce n’est pas grave, vous adoriez l’émission. Il n’est pas rare qu’on vous pose des questions car vous vous faites toujours un plaisir d’y répondre.</p>
                                <h4>Super compétence</h4>
                                <p>Transmettre ses connaissances.</p>
                                <h4>Pistes d'action</h4>
                                <ul>
                                    <li>Être mentor de lycéen·e·s ou étudiant·e·s</li>
                                    <li>Faire des ateliers pour vulgariser la science aux citoyens.</li>
                                    <li>Créer des médias d’information autour des enjeux actuels.</li>
                                    <li>Organiser des ateliers de réparation.</li>
                                </ul>
                            </div>

                            </div>
                        </div>
                        <div class='col col-sm-3 no-xs' id='results-nav-links' >
                            <div class="nav flex-column nav-pills" id="v-pills-tab" role="tablist" aria-orientation="vertical">
                                <a class="nav-link" :class="{active: this.indexMaxScore === 0}" id="v-pills-alerteur-tab" data-toggle="pill" href="#v-pills-alerteur" role="tab" aria-controls="v-pills-alerteur" aria-selected="true" @click="scrollUp">Alerteur</a>
                                <a class="nav-link" :class="{active: this.indexMaxScore === 1}" id="v-pills-bricoleur-tab" data-toggle="pill" href="#v-pills-bricoleur" role="tab" aria-controls="v-pills-bricoleur" aria-selected="false" @click="scrollUp">Bricoleur</a>
                                <a class="nav-link" :class="{active: this.indexMaxScore === 2}" id="v-pills-collaborateur-tab" data-toggle="pill" href="#v-pills-collaborateur" role="tab" aria-controls="v-pills-collaborateur" aria-selected="false" @click="scrollUp">Collaborateur</a>
                                <a class="nav-link" :class="{active: this.indexMaxScore === 3}" id="v-pills-ecolo-tab" data-toggle="pill" href="#v-pills-ecolo" role="tab" aria-controls="v-pills-ecolo" aria-selected="false" @click="scrollUp">Ecolo</a>
                                <a class="nav-link" :class="{active: this.indexMaxScore === 4}" id="v-pills-humaniste-tab" data-toggle="pill" href="#v-pills-humaniste" role="tab" aria-controls="v-pills-humaniste" aria-selected="false" @click="scrollUp">Humaniste</a>
                                <a class="nav-link" :class="{active: this.indexMaxScore === 5}" id="v-pills-pedagogue-tab" data-toggle="pill" href="#v-pills-pedagogue" role="tab" aria-controls="v-pills-pedagogue" aria-selected="false" @click="scrollUp">Pédagogue</a>
                            </div>
                        </div>
                        <ul class="nav nav-pills mb-3 no-sm" id="pills-tab" role="tablist">
                        <li class="nav-item">
                                <a class="nav-link" :class="{active: this.indexMaxScore === 0}" id="v-pills-alerteur-tab" data-toggle="pill" href="#v-pills-alerteur" role="tab" aria-controls="v-pills-alerteur" aria-selected="true" @click="scrollUp">Alerteur</a>
                        </li>
                        <li class="nav-item">
                                <a class="nav-link" :class="{active: this.indexMaxScore === 1}" id="v-pills-bricoleur-tab" data-toggle="pill" href="#v-pills-bricoleur" role="tab" aria-controls="v-pills-bricoleur" aria-selected="false" @click="scrollUp">Bricoleur</a>
                        </li>
                        <li class="nav-item">
                                <a class="nav-link" :class="{active: this.indexMaxScore === 2}" id="v-pills-collaborateur-tab" data-toggle="pill" href="#v-pills-collaborateur" role="tab" aria-controls="v-pills-collaborateur" aria-selected="false" @click="scrollUp">Collaborateur</a>
                        </li>
                        <li>
                                <a class="nav-link" :class="{active: this.indexMaxScore === 3}" id="v-pills-ecolo-tab" data-toggle="pill" href="#v-pills-ecolo" role="tab" aria-controls="v-pills-ecolo" aria-selected="false" @click="scrollUp">Ecolo</a>
                        </li>
                        <li>
                                <a class="nav-link" :class="{active: this.indexMaxScore === 4}" id="v-pills-humaniste-tab" data-toggle="pill" href="#v-pills-humaniste" role="tab" aria-controls="v-pills-humaniste" aria-selected="false" @click="scrollUp">Humaniste</a>
                        </li>
                        <li>
                                <a class="nav-link" :class="{active: this.indexMaxScore === 5}" id="v-pills-pedagogue-tab" data-toggle="pill" href="#v-pills-pedagogue" role="tab" aria-controls="v-pills-pedagogue" aria-selected="false" @click="scrollUp">Pédagogue</a>
                        </li>
                        </ul>
                    </div>
                </div>
            </div> 
        </div>
                <div id="retry-xs" class="no-sm">
                    <button class='btn btn-primary'  @click='retry'>Recommencer le test</button>
                </div>
       
        
    </div>
    
</template>

<script>
import Chart from 'chart.js';
    export default{
        props: {
            scores:Array
        },
        methods: {
            createChart(chartId, chartData) {
                const ctx = document.getElementById(chartId);
                // eslint-disable-next-line
                const myChart = new Chart(ctx, {
                type: chartData.type,
                data: chartData.data,
                options: chartData.options,
                });
                return myChart;
            },
            retry(){
                this.$emit('retry');
            },
            scrollUp(){
                document.getElementById('results-explanations').scrollTop = 0;
            }
        },
        mounted() {
        this.myChart = this.createChart('spider-chart', this.chartData);
        },
        data() {
            return {
            profilLabels: ['Alerteur', 'Bricoleur', 'Collaborateur', 'Ecolo', 'Humaniste', 'Pédagogue'],
            myChart:'',
            chartData: {
                type: 'radar',
                data: {
                    labels: ['Alerteur', 'Bricoleur', 'Collaborateur', 'Ecolo', 'Humaniste', 'Pédagogue'],
                    datasets: [{
                        data: this.scores,
                        backgroundColor: 'rgba(182,206,40,.5)',
                    }]
                },
                options : {
                    responsive: true,
                    scale:{
                        ticks:{
                            display:false,
                            min:0,
                            max:1
                        },
                        angleLines:{
                            color:'white'
                        },
                        gridLines:{
                            color:'white'
                        },
                        pointLabels:{
                            fontColor: 'white',
                        },
                    },
                    legend:{
                        display:false
                    }
                }
            }
            }
        },
        computed:{
            indexMaxScore(){
                return this.scores.indexOf(Math.max(...this.scores));
            }
        }
    }   
</script>

<style>

@media (max-width:768px){
    .no-xs{
        display:none;
    }

    .no-sm.nav-pills .nav-link{
        font-size:0.8rem;
    }

    #results-explanations p, #results-explanations li{
        font-size:0.9rem;
    }
    #retry-xs{
        text-align:center;
    }

    #retry-xs .btn{
        margin-top:1rem;
    }


    .col-graph{
        padding:1rem;
    }

    .col-graph h4{
       font-size:1.2rem;

    }
    #results-explanations {
    background-color:rgba(255, 255, 255, 1);
    color:rgb(83, 83, 83);
    height:45vh;
    padding:1rem !important;
    overflow:auto;
    }
    .nav-pills .nav-link.active{
      background-color:rgb(17, 82, 179);
      border-bottom: 0.2em solid #b6ce28;
      border-radius:0;
    }

    a.nav-link{
        color:white;
    }

}
@media (min-width:768px){
    .no-sm{
        display:none;
    }

    .col-graph{
        padding-top: 2em;
    }
    #results-explanations {
    background-color:rgba(255, 255, 255, 1);
    color:rgb(83, 83, 83);
    padding: 2em !important;
    height:70vh;
    overflow:auto;
    }

    .nav-pills .nav-link.active{
      background-color:#0D47A1;
      border-right: 0.2em solid #b6ce28;
      border-radius:0;
    }

    a.nav-link{
        color:white;
    }
    a.nav-link:hover{
        color:rgb(207, 207, 207);
    }

    #results-nav-links{
        padding-right:0;
    }



    #div-retry{
        position:absolute;
        bottom:1em;
        left:1em;
    }
}


#results .col{
    padding-right:0;
    padding-left:0;
}

#results-explanations h4{
    font-size: 1rem;
    font-weight: bold;
    color: rgb(63, 63, 63);
}

#results-explanations h3{
    text-transform: uppercase;
    color: rgb(39, 75, 129);
    font-weight: bold;
    font-size:1.6rem;
    text-align:center;
}
#results-explanations p{
    text-align:justify;
}

#results>.row{
    background: linear-gradient(to bottom right, #0D47A1,rgb(6, 32, 71));
}




#results-explanations img.long{
    width:70%;
}

#results .btn-primary{
    background-color : white;
    color:rgb(83, 83, 83);;
    border:none;
    font-weight:bold;
    border-top : 0.2em solid  white;
    border-bottom : 0.3em solid  white; 
    border-radius:0;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.5);
    transition: color 0.15s ease-in-out,border-color 0.3s ease-in-out;
}

#results .btn-primary:hover{
    border-bottom : 0.3em solid  #b6ce28; 

}

.col-graph h4{
    text-align: center;
    margin-bottom: 2rem;
}

</style>
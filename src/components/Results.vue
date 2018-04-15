<template>
    <div class='container' id='results'>
        <div class='row'>
            <div class="col-sm col-graph">
                    <canvas id="spider-chart"></canvas>
            </div>
            <div class="col-sm col-explanations">
                <div class='container-fluid'>
                    <div class='row' id='results-explanations'>
                        <div class='col-sm-9'>
                            <div class="tab-content" id="v-pills-tabContent">
                            <div class="tab-pane fade" :class="{show : this.indexMaxScore === 0, active: this.indexMaxScore === 0}" id="v-pills-alerteur" role="tabpanel" aria-labelledby="v-pills-alerteur-tab">
                                <h3>L'alerteur</h3>
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
                                <h3>Le bricoleur</h3>
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
                                <h3>Le collaborateur</h3>
                                <h4>Caractéristiques</h4>
                                <p>Vous adorez travailler en équipe. Pour vous seul on va peut être plus vite mais à plusieurs on va plus loin. Votre ingéniosité est multipliée quand vous réfléchissez à plusieurs et il vous parait dommage de garder une idée pour soi surtout quand elle a un impact social positif.</p>
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
                            <div class="tab-pane fade" :class="{show : this.indexMaxScore === 3, active: this.indexMaxScore === 3}" id="v-pills-ecolo" role="tabpanel" aria-labelledby="v-pills-ecolo-tab">d</div>
                            <div class="tab-pane fade" :class="{show : this.indexMaxScore === 4, active: this.indexMaxScore === 4}" id="v-pills-humaniste" role="tabpanel" aria-labelledby="v-pills-humaniste-tab">e</div>
                            <div class="tab-pane fade" :class="{show : this.indexMaxScore === 5, active: this.indexMaxScore === 5}" id="v-pills-pedagogue" role="tabpanel" aria-labelledby="v-pills-pedagogue-tab">e</div>

                            </div>
                        </div>
                        <div class='col-sm-3' id='results-nav-links' >
                            <div class="nav flex-column nav-pills" id="v-pills-tab" role="tablist" aria-orientation="vertical">
                                <a class="nav-link" :class="{active: this.indexMaxScore === 0}" id="v-pills-alerteur-tab" data-toggle="pill" href="#v-pills-alerteur" role="tab" aria-controls="v-pills-alerteur" aria-selected="true">Alerteur</a>
                                <a class="nav-link" :class="{active: this.indexMaxScore === 1}" id="v-pills-bricoleur-tab" data-toggle="pill" href="#v-pills-bricoleur" role="tab" aria-controls="v-pills-bricoleur" aria-selected="false">Bricoleur</a>
                                <a class="nav-link" :class="{active: this.indexMaxScore === 2}" id="v-pills-collaborateur-tab" data-toggle="pill" href="#v-pills-collaborateur" role="tab" aria-controls="v-pills-collaborateur" aria-selected="false">Collaborateur</a>
                                <a class="nav-link" :class="{active: this.indexMaxScore === 3}" id="v-pills-ecolo-tab" data-toggle="pill" href="#v-pills-ecolo" role="tab" aria-controls="v-pills-ecolo" aria-selected="false">Ecolo</a>
                                <a class="nav-link" :class="{active: this.indexMaxScore === 4}" id="v-pills-humaniste-tab" data-toggle="pill" href="#v-pills-humaniste" role="tab" aria-controls="v-pills-humaniste" aria-selected="false">Humaniste</a>
                                <a class="nav-link" :class="{active: this.indexMaxScore === 5}" id="v-pills-pedagogue-tab" data-toggle="pill" href="#v-pills-pedagogue" role="tab" aria-controls="v-pills-pedagogue" aria-selected="false">Pédagogue</a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
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
            crcollaborateureChart(chartId, chartData) {
                const ctx = document.getElementById(chartId);
                // eslint-disable-next-line
                const myChart = new Chart(ctx, {
                type: chartData.type,
                data: chartData.data,
                options: chartData.options,
                });
                return myChart;
            }
        },
        mounted() {
        this.myChart = this.crcollaborateureChart('spider-chart', this.chartData);
        },
        data() {
            return {
            myChart:'',
            chartData: {
                type: 'radar',
                data: {
                    labels: ['Alerteur', 'Bricoleur', 'Collaborateur', 'Ecolo', 'Humaniste', 'Pédagogue'],
                    datasets: [{
                        label:'Mon profil',
                        data: this.scores,
                        backgroundColor: 'rgba(252,171,28,.5)',
                    }]
                },
                options : {
                    responsive: true,
                    scale:{
                        ticks:{
                            display:false,
                            min:0,
                            max:10
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
#results-explanations {
    border:solid 1px white;
    background-color:white;
    color:grey;
}

.nav-pills .nav-link.active{
      background-color:#b6ce28;
}

a.nav-link{
    color:#b6ce28;
}
a.nav-link:hover{
    color:#9aaf22;
}

#results-nav-links{
    padding-right:0;
}

</style>
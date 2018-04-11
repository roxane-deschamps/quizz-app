<template>
    <div class='container' id='results'>
        <div class='row'>
            <div class="col-sm">
                <h1>Ton profil</h1>
                    <canvas id="spider-chart"></canvas>
            </div>
        </div>
       
        <div class='row' id='results-explanations'>
            <div class='col-sm-9'>
                <div class="tab-content" id="v-pills-tabContent">
                <div class="tab-pane fade" :class="{show : this.indexMaxScore === 0, active: this.indexMaxScore === 0}" id="v-pills-running" role="tabpanel" aria-labelledby="v-pills-running-tab">
                    <h3>Running</h3>
                    Blablbauyfyatdyrdayr
                </div>
                <div class="tab-pane fade" :class="{show : this.indexMaxScore === 1, active: this.indexMaxScore === 1}" id="v-pills-swim" role="tabpanel" aria-labelledby="v-pills-swim-tab">b</div>
                <div class="tab-pane fade" :class="{show : this.indexMaxScore === 2, active: this.indexMaxScore === 2}" id="v-pills-eat" role="tabpanel" aria-labelledby="v-pills-eat-tab">c</div>
                <div class="tab-pane fade" :class="{show : this.indexMaxScore === 3, active: this.indexMaxScore === 3}" id="v-pills-cycling" role="tabpanel" aria-labelledby="v-pills-cycling-tab">d</div>
                <div class="tab-pane fade" :class="{show : this.indexMaxScore === 4, active: this.indexMaxScore === 4}" id="v-pills-sleep" role="tabpanel" aria-labelledby="v-pills-sleep-tab">e</div>
                </div>
            </div>
            <div class='col-sm-3' id='results-nav-links' >
                <div class="nav flex-column nav-pills" id="v-pills-tab" role="tablist" aria-orientation="vertical">
                    <a class="nav-link" :class="{active: this.indexMaxScore === 0}" id="v-pills-running-tab" data-toggle="pill" href="#v-pills-running" role="tab" aria-controls="v-pills-running" aria-selected="true">Running</a>
                    <a class="nav-link" :class="{active: this.indexMaxScore === 1}" id="v-pills-swim-tab" data-toggle="pill" href="#v-pills-swim" role="tab" aria-controls="v-pills-swim" aria-selected="false">Swimming</a>
                    <a class="nav-link" :class="{active: this.indexMaxScore === 2}" id="v-pills-eat-tab" data-toggle="pill" href="#v-pills-eat" role="tab" aria-controls="v-pills-eat" aria-selected="false">Eating</a>
                    <a class="nav-link" :class="{active: this.indexMaxScore === 3}" id="v-pills-cycling-tab" data-toggle="pill" href="#v-pills-cycling" role="tab" aria-controls="v-pills-cycling" aria-selected="false">Cycling</a>
                    <a class="nav-link" :class="{active: this.indexMaxScore === 4}" id="v-pills-sleep-tab" data-toggle="pill" href="#v-pills-sleep" role="tab" aria-controls="v-pills-sleep" aria-selected="false">Sleeping</a>
                </div>
            </div>
         </div>
    </div>
    
</template>

<script>
import Chart from 'chart.js';
    export default{
        props: {
            scores:Object
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
    
            }
        },
        mounted() {
        this.createChart('spider-chart', this.chartData);
        },
        data() {
            return {
            chartData: {
                type: 'radar',
                data: {
                    labels: ['Running', 'Swimming', 'Eating', 'Cycling', 'Sleeping'],
                    datasets: [{
                        label:'Mon profil',
                        data: this.scores,
                        backgroundColor: 'rgba(0,73,93,.5)'
                    }]
                },
                options : {
                    responsive: true,
                    scale:{
                        ticks:{
                            display:false,
                            min:0,
                            max:10
                        }
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
    color:green;
}

#results-nav-links{
    padding-right:0;
}

</style>
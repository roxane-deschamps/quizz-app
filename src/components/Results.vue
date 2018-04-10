<template>
    <div>
 Results
        <canvas id="spider-chart"></canvas>
    </div>
    
</template>

<script>
import Chart from 'chart.js';
    export default{
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
                        data: [20, 10, 4, 2]
                    }]
                }
            }
        }
        }}
    
</script>

<style>
</style>
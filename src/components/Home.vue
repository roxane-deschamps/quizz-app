<template>
    <div>
        <h1>L'ingénieurie positive by Isa</h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer tristique urna id fringilla sollicitudin. Nulla varius hendrerit lorem, vel ultrices lectus scelerisque eget. Morbi iaculis sed justo et dignissim. Mauris interdum fermentum massa et mattis. Donec placerat tortor vitae mauris efficitur viverra. Duis rutrum, arcu eget volutpat lobortis, felis orci sollicitudin libero, sit amet venenatis quam justo id tellus. Nulla fermentum tellus eget facilisis dignissim.</p>
        <button @click='beginTest'>Faire le test</button>
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
</style>
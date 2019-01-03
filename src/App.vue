<template>
    <div id="app">
        <img alt="Vue logo" src="./assets/logo.png">
        <h3>Image with preview</h3>
        <VueImage alt="Test img" width="500px" height="375px"
                  full="https://ucarecdn.com/b86e2dd6-fb4d-49bb-93ff-86b596a69fcb/-/resize/500x/cave.jpg"
                  preview="https://ucarecdn.com/b86e2dd6-fb4d-49bb-93ff-86b596a69fcb/-/resize/32x/-/quality/lightest/cave.jpg"></VueImage>
        <VueImage alt="Test img" width="500px" height="375px"
                  full="httpsxxx://ucarecdn.com/b86e2dd6-fb4d-49bb-93ff-86b596a69fcb/-/resize/500x/cave.jpg"
                  preview="https://ucarecdn.com/b86e2dd6-fb4d-49bb-93ff-86b596a69fcb/-/resize/32x/-/quality/lightest/cave.jpg"></VueImage>
        <h3>Image with spinner</h3>
        <VueImage alt="Test img" width="500px" height="375px"
                  full="https://ucarecdn.com/b86e2dd6-fb4d-49bb-93ff-86b596a69fcb/-/resize/500x/cave.jpg"></VueImage>
        <VueImage alt="Test img" width="500px" height="375px"
                  full="httpsss://ucarecdn.com/b86e2dd6-fb4d-49bb-93ff-86b596a69fcb/-/resize/500x/cave.jpg"></VueImage>
    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import VueImage from './components/VueImage.vue';

    @Component({
        components: {
            VueImage,
        },
    })
    export default class App extends Vue {
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    .img-wrapper {
        margin: auto;
    }
</style>

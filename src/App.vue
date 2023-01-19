<script>
import AppNav from './components/AppNav.vue';
import AppMain from './components/AppMain.vue';
import axios from 'axios';
export default {
    components: {
        AppNav,
        AppMain
    },

}


</script>

<template>
    <AppNav></AppNav>
    <AppMain></AppMain>
</template>

<style lang="scss">
@use './styles/general.scss';
</style>

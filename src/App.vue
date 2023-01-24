<script>
import AppNav from './components/AppNav.vue';
import AppFooter from './components/AppFooter.vue';

export default {
    components: {
        AppNav, AppFooter
    },

}


</script>

<template>
    <AppNav></AppNav>
    <router-view></router-view>
    <AppFooter />
</template>

<style lang="scss">
@use './styles/general.scss';
</style>

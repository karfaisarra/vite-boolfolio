<script>
import AppNav from './components/AppNav.vue';
import ProjectCard from './components/ProjectCard.vue';

export default {
    components: {
        AppNav,
        ProjectCard
    },

}


</script>

<template>
    <AppNav></AppNav>
    <ProjectCard></ProjectCard>
</template>

<style lang="scss">
@use './styles/general.scss';
</style>

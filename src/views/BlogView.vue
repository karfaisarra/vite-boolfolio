<script>
import AppBanner from '../components/AppBanner.vue';
import ProjectCard from '../components/ProjectCard.vue';

export default {
    name: 'BlogView',
    components: {
        ProjectCard, AppBanner
    }
}
</script>

<template>
    <AppBanner title="Projects" />
    <ProjectCard />
</template>

<style lang="scss" scoped>

</style>
<script>
import AppBanner from '../components/AppBanner.vue';
import ProjectsList from '../components/ProjectsList.vue';

export default {
    name: 'BlogView',
    components: {
        ProjectsList, AppBanner
    }
}
</script>

<template>
    <AppBanner title="Projects" />
    <ProjectsList />
</template>

<style lang="scss" scoped>

</style>
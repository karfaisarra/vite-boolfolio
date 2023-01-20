<script>
import AppBanner from '../components/AppBanner.vue';
import axios from 'axios'
export default {
    name: 'SingleProjectView',
    components: {
        AppBanner
    },
    data() {
        return {
            project: [],
            loading: true,
            api_base_url: 'http://127.0.0.1:8000'
        }
    },
    methods: {
        getSingleProject(url) {
            axios
                .get(url)
                .then(response => {
                    console.log(response.data.results);
                    this.project = response.data.results;
                })
                .catch(error => {
                    console.error(error)
                    this.error = error.message
                })
        },
        getImageUrl(imageUrl) {
            if (imageUrl) {
                return this.api_base_url + '/storage/' + imageUrl
            }
            return '/img/notfound.png'
        }
    },
    mounted() {
        const url = this.api_base_url + '/api/projects/' + this.$route.params.slug
        this.getSingleProject(url)
    }
}
</script>

<template>
    <AppBanner :title="$route.params.slug" />
    <div class="container d-flex gap-4 my-5">
        <img :src="getImageUrl(project.cover_image)" alt="">
        <div class="details">
            <h4>{{ project.title }}</h4>
            <p>{{ project.description }}</p>
            <div class="type">
                <strong>Type: </strong>
                <span v-if="project.type">{{ project.type.name }}</span>
                <span v-else>Untyped</span>
            </div>
            <!-- <div class="technologies">
                <strong>Technologies: </strong>
                <template v-if="project.technologies.length > 0">
                    <span v-for="technology in project.technologies">
                        {{ technology.name }}/
                    </span>
                </template>
                <template v-else>
                    <span>No technologies in this project.</span>
                </template>
            </div> -->
        </div>
    </div>
</template>

<style lang="scss" scoped>

</style>
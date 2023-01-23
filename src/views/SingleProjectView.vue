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
            api_base_url: 'http://127.0.0.1:8000',
            loading: true
        }
    },
    methods: {
        getSingleProject(url) {
            axios
                .get(url)
                .then(response => {
                    console.log(response.data.results);
                    this.project = response.data.results;
                    this.loading = false
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
    <div class="container d-flex gap-4 my-5" v-if="project && !loading">
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
    <div v-else-if="loading" class="text-center mt-5">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-hourglass-split"
            viewBox="0 0 16 16">
            <path
                d="M2.5 15a.5.5 0 1 1 0-1h1v-1a4.5 4.5 0 0 1 2.557-4.06c.29-.139.443-.377.443-.59v-.7c0-.213-.154-.451-.443-.59A4.5 4.5 0 0 1 3.5 3V2h-1a.5.5 0 0 1 0-1h11a.5.5 0 0 1 0 1h-1v1a4.5 4.5 0 0 1-2.557 4.06c-.29.139-.443.377-.443.59v.7c0 .213.154.451.443.59A4.5 4.5 0 0 1 12.5 13v1h1a.5.5 0 0 1 0 1h-11zm2-13v1c0 .537.12 1.045.337 1.5h6.326c.216-.455.337-.963.337-1.5V2h-7zm3 6.35c0 .701-.478 1.236-1.011 1.492A3.5 3.5 0 0 0 4.5 13s.866-1.299 3-1.48V8.35zm1 0v3.17c2.134.181 3 1.48 3 1.48a3.5 3.5 0 0 0-1.989-3.158C8.978 9.586 8.5 9.052 8.5 8.351z" />
        </svg>
        Loading...
    </div>
</template>

<style lang="scss" scoped>

</style>
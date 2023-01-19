<script>
import axios from 'axios';
export default {
    name: 'AppMain',
    data() {
        return {
            projects: {},
            api_url: 'http://127.0.0.1:8000',
            error: null,
            max: 100
        }
    },
    methods: {
        getProject(url) {
            axios
                .get(url)
                .then(response => {
                    console.log(response.data.results);
                    this.projects = response.data.results;
                })
                .catch(error => {
                    console.error(error)
                    this.error = error.message
                })
        },
        getImageUrl(imageUrl) {
            //console.log(imageUrl);
            if (imageUrl) {
                return this.api_url + '/storage/' + imageUrl
            }
            return '/img/notfound.png'
        },
        sliceDescription(text) {
            if (text.length > this.max) {
                return text.slice(0, this.max) + '...'
            }
        }
    },
    mounted() {
        this.getProject(this.api_url + '/api/projects');
    }
}


</script>

<template>

    <section class="vue-home">
        <div class="container py-5">
            <h1 class="pb-4">All Projects</h1>
            <div class="row row-cols-3 g-4">
                <div class="col" v-for="project in projects.data">
                    <div class="card">
                        <img class="card-image-top" :src="getImageUrl(project.cover_image)" alt="">
                        <div class="card-body">
                            <h5>{{ project.title }}</h5>
                            <p>{{ sliceDescription(project.description) }}</p>
                        </div>
                        <div class="card-footer">
                            <div class="type">
                                <strong>Type: </strong>
                                <span v-if="project.type">{{ project.type.name }}</span>
                                <span v-else>Untyped</span>
                            </div>
                            <div class="technologies">
                                <strong>Technologies: </strong>
                                <template v-if="project.technologies.length > 0">
                                    <span v-for="technology in project.technologies">
                                        {{ technology.name }}/
                                    </span>
                                </template>
                                <template v-else>
                                    <span>No technologies in this project.</span>
                                </template>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<style lang="scss" scoped>

</style>
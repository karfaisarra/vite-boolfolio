<script>
import { state } from '../state.js'

export default {
    name: 'ProjectCard',
    props: {
        project: Object
    },
    data() {
        return {
            state,
            max: 100,
        }
    },
    methods: {
        getImageUrl(imageUrl) {
            //console.log(imageUrl);
            if (imageUrl) {
                return this.state.api_url + '/storage/' + imageUrl
            }
            return '/img/notfound.png'
        },
        sliceDescription(text) {
            if (text.length > this.max) {
                return text.slice(0, this.max) + '...'
            }
        }
    }
}
</script>
<template>
    <div class="col">
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
                <router-link :to="{ name: 'single-project', params: { slug: project.slug } }"> Read
                    More</router-link>
            </div>
        </div>
    </div>
</template>
<style lang="scss" scoped>

</style>
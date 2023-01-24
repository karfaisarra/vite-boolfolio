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
        <div class=" card border-0 bg-transparent " style="height: 500px">
            <div class="my_card rounded-3 ">
                <img height="200" class="card-image-top w-100 rounded-top" :src="getImageUrl(project.cover_image)"
                    alt="">
                <div class="card-body ">
                    <h5>{{ project.title }}</h5>
                    <p>{{ sliceDescription(project.description) }}</p>
                </div>
                <div class="card-footer p-3 bg-transparent border-0">
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
                    <div class="mt-3">
                        <router-link :to="{ name: 'single-project', params: { slug: project.slug } }"
                            class="my_btn rounded ">
                            Read More
                        </router-link>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style lang="scss" scoped>
.my_card {
    background-color: #cce9d3;
}

.my_btn {
    text-decoration: none;
    background-color: #396544;
    color: white;
    padding: 0.4rem;

    &:hover {
        background-color: #568662;
    }

}
</style>
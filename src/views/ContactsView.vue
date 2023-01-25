<script>
import { state } from '../state.js';
import axios from 'axios';
import AppBanner from '../components/AppBanner.vue';

export default {
    name: 'ContactsView',
    components: {
        AppBanner
    },
    data() {
        return {
            state,
            name: '',
            email: '',
            message: '',
            success: false,
            loading: false,
            errors: {}
        }
    },
    methods: {
        sendForm() {
            this.loading = true
            const data = {
                name: this.name,
                email: this.email,
                message: this.message,
            }
            axios
                .post(`${this.state.api_url}/api/contacts`, data)
                .then(response => {
                    this.success = response.data.success
                    console.log(response);
                    if (this.success) {
                        this.name = ''
                        this.email = ''
                        this.message = ''
                        this.errors = {}
                    } else {
                        this.errors = response.data.errors;
                    }
                    this.loading = false
                })

        }
    }
}
</script>

<template>
    <AppBanner title="Contacts" />
    <div class="container bg-light p-4 rounded-1 shadow-lg my-5">

        <p class="lead">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Libero, adipisci optio, tempore maiores sit
            asperiores
            sed est nulla esse quos quam laudantium, voluptatibus minus officiis assumenda. Ex vitae eos earum.
        </p>

        <div v-if="success" class="alert alert-success text-start" role="alert">
            Form inviato con successo!
        </div>

        <form @submit.prevent="sendForm()">
            <div v-if="!loading">
                <div class="mb-3">
                    <label for="" class="form-label">Full Name</label>
                    <input type="text" name="name" id="name" v-model="name" class="form-control"
                        placeholder="Mario Rossi" aria-describedby="fullNameHelper">
                    <small id="fullNameHelper" class="text-muted">Add your full name</small>
                    <div class="alert alert-danger" role="alert" v-for="error in errors.name">
                        {{ error }}
                    </div>
                </div>
                <div class="mb-3">
                    <label for="" class="form-label">Email</label>
                    <input type="email" name="email" id="email" v-model="email" class="form-control"
                        placeholder="mario.rossi@example.com" aria-describedby="emailHelper">
                    <small id="emailHelper" class="text-muted">Add your email address</small>
                    <div class="alert alert-danger" role="alert" v-for="error in errors.email">
                        {{ error }}
                    </div>
                </div>

                <div class="mb-3">
                    <label for="" class="form-label">Message</label>
                    <textarea class="form-control" name="message" id="message" v-model="message" rows="5"></textarea>
                    <div class="alert alert-danger" role="alert" v-for="error in errors.message">
                        {{ error }}
                    </div>
                </div>
            </div>
            <div v-else class="text-center my-5">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                    class="bi bi-hourglass-split" viewBox="0 0 16 16">
                    <path
                        d="M2.5 15a.5.5 0 1 1 0-1h1v-1a4.5 4.5 0 0 1 2.557-4.06c.29-.139.443-.377.443-.59v-.7c0-.213-.154-.451-.443-.59A4.5 4.5 0 0 1 3.5 3V2h-1a.5.5 0 0 1 0-1h11a.5.5 0 0 1 0 1h-1v1a4.5 4.5 0 0 1-2.557 4.06c-.29.139-.443.377-.443.59v.7c0 .213.154.451.443.59A4.5 4.5 0 0 1 12.5 13v1h1a.5.5 0 0 1 0 1h-11zm2-13v1c0 .537.12 1.045.337 1.5h6.326c.216-.455.337-.963.337-1.5V2h-7zm3 6.35c0 .701-.478 1.236-1.011 1.492A3.5 3.5 0 0 0 4.5 13s.866-1.299 3-1.48V8.35zm1 0v3.17c2.134.181 3 1.48 3 1.48a3.5 3.5 0 0 0-1.989-3.158C8.978 9.586 8.5 9.052 8.5 8.351z" />
                </svg>
                Loading...
            </div>

            <button type="submit" class="btn btn-primary " :disabled="loading"> {{
                loading? 'Sending...':
                    'Contact Me'
            }}
            </button>
        </form>
    </div>
</template>

<style lang="scss" scoped>

</style>
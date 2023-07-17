<script>

import axios from 'axios';
import { store } from '../data/store';

export default {
    name: "AppMain",
    components: {

    },
    data() {
        return {
            store,
            apiUrl: "http://localhost:8000/api/",
            loading: false,
            loadingError: false,
            projects: [],
        }
    },
    methods: {
        getProjectsFirstPage() {

            this.loading = true;
            axios.get(this.apiUrl + "projects").then(response => {
                console.log(response.data);
                this.projects = response.data.results;
                this.projectsCurrentPage = response.data.results.current_page;
                this.projectsTotalPages = response.data.results.last_page;
                this.loading = false;
            }).catch(err => {
                this.loading = false;
                this.loadingError = err.message;
            });

        },
    },
    mounted() {
        this.getProjectsFirstPage();
    }
}
</script>

<template>
    <div class="container d-flex flex-wrap gap-3">
        <div v-for="project in projects">
            <div class="card" style="width: 18rem;">
                <img src="" class="card-img-top" alt="...">
                <div class="card-body">
                    <h5 class="card-title">{{ project.title }}</h5>
                    <p class="card-text">{{ project.description }}.</p>
                    <a href="#" class="btn btn-primary">Go somewhere</a>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
@use '../variables.scss' as *;
</style>
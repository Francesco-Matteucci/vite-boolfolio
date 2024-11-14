<script>
    import axios from 'axios';

    export default {
        name: 'AppMain',
        data() {
            return {
                projects: [],
                loading: true,
                error: null,
            };
        },
        created() {
            this.fetchProjects();
        },
        methods: {
            async fetchProjects() {
                try {
                    const response = await axios.get('http://127.0.0.1:8000/api/projects');
                    this.projects = response.data.data;
                } catch (error) {
                    this.error = 'Failed to load projects. Please try again later.';
                } finally {
                    this.loading = false;
                }
            },
        },
    };
</script>

<template>
    <div class="container mt-5">
        <h1 class="text-center mb-4">Boolfolio Projects</h1>
        <div v-if="loading" class="text-center">
            <p>Caricamento dei progetti...</p>
        </div>
        <div v-else>
            <div v-if="error" class="alert alert-danger">
                {{ error }}
            </div>
            <div v-else>
                <div class="row g-4">
                    <div v-for="project in projects" :key="project.id" class="col-md-4">
                        <div class="card h-100 shadow-sm">
                            <div class="card-body d-flex flex-column">
                                <h5 class="card-title">{{ project.title }}</h5>
                                <p class="card-text flex-grow-1">{{ project.description }}</p>
                                <a :href="project.url" target="_blank" class="btn btn-primary mt-auto">
                                    Vedi il progetto su GitHub
                                </a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .card {
        border-radius: 10px;
        overflow: hidden;
    }

    .card-title {
        font-size: 1.25rem;
        font-weight: bold;
    }

    .card-text {
        font-size: 0.95rem;
        color: #6c757d;
    }
</style>
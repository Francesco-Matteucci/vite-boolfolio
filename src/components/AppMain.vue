<script>
    import axios from 'axios';
    import ProjectCard from './ProjectCard.vue';

    export default {
        name: 'AppMain',
        data() {
            return {
                projects: [],
                selectedProject: null,
                loading: true,
                error: null,
            };
        },
        components: {
            ProjectCard,
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
            viewDetails(project) {
                this.selectedProject = project;
            },
            closeDetails() {
                this.selectedProject = null;
            },
        },
    };
</script>

<template>
    <div class="container mt-5">
        <h1 class="text-center mb-4">Boolfolio dei Progetti di Francesco Matteucci</h1>
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
                        <div class="card h-100 shadow-lg">
                            <div class="card-body d-flex flex-column">
                                <h5 class="card-title text-primary">{{ project.title }}</h5>
                                <p class="card-text flex-grow-1">{{ project.description }}</p>
                                <p class="card-text">
                                    <strong>Tipo: </strong>
                                    <span class="badge bg-info text-dark">{{ project.type.name }}</span>
                                </p>

                                <div class="mt-auto">
                                    <a :href="project.url" target="_blank" class="btn btn-success mt-3">
                                        Vai al Progetto
                                    </a>
                                    <button class="btn btn-secondary mt-3 ms-3" @click="viewDetails(project)">
                                        Dettagli
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <ProjectCard v-if="selectedProject" :project="selectedProject" @close="closeDetails" />
    </div>
</template>

<style scoped>
    .card {
        border-radius: 10px;
    }

    .card-title {
        font-size: 1.25rem;
        font-weight: bold;
    }

    .card-text {
        font-size: 0.95rem;
        color: #6c757d;
    }

    .badge {
        font-size: 0.85rem;
    }
</style>
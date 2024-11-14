<script>
    export default {
        name: 'ProjectCard',
        props: {
            project: {
                type: Object,
                required: true,
            },
        },
        methods: {
            close() {
                this.$emit('close');
            },
        },
    };
</script>

<template>
    <div class="modal d-flex align-items-center justify-content-center" tabindex="-1"
        style="display: block; background: rgba(0, 0, 0, 0.8);">
        <div class="modal-dialog modal-lg">
            <div class="modal-content shadow-lg">
                <div class="modal-header bg-primary text-white">
                    <h5 class="modal-title">{{ project.title }}</h5>
                    <button type="button" class="btn-close btn-close-white" aria-label="Close" @click="close"></button>
                </div>
                <div class="modal-body p-4">
                    <div class="row">
                        <div class="col-12">
                            <p>
                                <strong>Descrizione:</strong>
                                <br>
                                {{ project.description }}
                            </p>
                            <p>
                                <strong>Tipo: </strong>
                                <span class="badge bg-info text-dark">{{ project.type ? project.type.name : 'N/A'
                                    }}</span>
                            </p>
                            <p>
                                <strong>Tecnologia utilizzate:</strong>
                            </p>
                            <ul class="list-inline">
                                <li v-for="tech in project.technologies" :key="tech.id" class="list-inline-item">
                                    <span class="badge bg-secondary">{{ tech.name }}</span>
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <a :href="project.url" class="btn btn-success" target="_blank">
                        Vedi su GitHub
                    </a>
                    <button type="button" class="btn btn-secondary" @click="close">
                        Chiudi dettaglio
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .modal {
        position: fixed;
        top: 0;
        left: 0;
        backdrop-filter: blur(5px);
    }

    .modal-content {
        border-radius: 15px;
    }

    .modal-body {
        background: #f8f9fa;
        color: #212529;
        border-radius: 10px;
    }
</style>
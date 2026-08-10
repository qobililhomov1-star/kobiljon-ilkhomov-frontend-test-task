<script setup>
defineProps({
    project: {
        type: Object,
        required: true,
    },
})
</script>

<template>
    <div class="project-card">
        <div class="project-card__icon">
            {{ project.name.charAt(0) }}
        </div>
        <div>
            <h3>{{ project.name }}</h3>
            <p>{{ project.description }}</p>
        </div>
    </div>
</template>

<style scoped>
.project-card {
    display: flex;
    gap: 14px;
    padding: 18px;
    border: 1px solid #e5e7eb;
    border-radius: 10px;
}

.project-card__icon {
    width: 40px;
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-shrink: 0;
    border-radius: 8px;
    background: #eef2ff;
    color: #4f46e5;
    font-weight: bold;
}

.project-card h3 {
    margin: 0 0 6px;
    font-size: 16px;
}

.project-card p {
    margin: 0;
    color: #6b7280;
    font-size: 14px;
}
</style>
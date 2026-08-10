<script setup>
import { onMounted, onUnmounted, ref } from 'vue'
import ProjectCard from '@/components/ProjectCard.vue'

const projects = [
    {
        id: 1,
        name: 'CRM Platform',
        description: 'Customer relationship management system',
    },
    {
        id: 2,
        name: 'Mobile Application',
        description: 'Mobile application for team members',
    },
    {
        id: 3,
        name: 'Analytics Dashboard',
        description: 'Business analytics and reporting',
    },
    {
        id: 4,
        name: 'Payment System',
        description: 'Online payment integration',
    },
    {
        id: 5,
        name: 'Design System',
        description: 'Reusable UI component library',
    },
    {
        id: 6,
        name: 'Marketing Website',
        description: 'Corporate marketing website',
    },
    {
        id: 7,
        name: 'Task Manager',
        description: 'Task and project management tool',
    },
    {
        id: 8,
        name: 'Notification Service',
        description: 'Centralized notification service',
    },
    {
        id: 9,
        name: 'Reporting System',
        description: 'Automated reporting system',
    },
    {
        id: 10,
        name: 'Internal Portal',
        description: 'Internal company workspace',
    },
]

const visibleProjects = ref([])
let rotationInterval = null

function getRandomProjects() {
    const shuffled = [...projects]

    for (let i = shuffled.length - 1; i > 0; i--) {
        const randomIndex = Math.floor(Math.random() * (i + 1))

        ;[shuffled[i], shuffled[randomIndex]] = [
            shuffled[randomIndex],
            shuffled[i],
        ]
    }

    return shuffled.slice(0, 2)
}

function rotateProjects() {
    let next
    do {
        next = getRandomProjects()
    } while (
        visibleProjects.value.length &&
        next.every(p => visibleProjects.value.some(v => v.id === p.id))
        )
    visibleProjects.value = next
}

onMounted(() => {
    rotateProjects()

    rotationInterval = setInterval(rotateProjects, 5000)
})

onUnmounted(() => {
    clearInterval(rotationInterval)
})
</script>

<template>
    <section class="projects">
        <div class="projects__header">
            <div>
                <h2>Active projects</h2>
                <p>Current projects of the team</p>
            </div>

            <span class="projects__counter">
                2 of {{ projects.length }}
            </span>
        </div>

        <div class="projects__list">
            <ProjectCard
                v-for="project in visibleProjects"
                :key="project.id"
                :project="project"
            />
        </div>
    </section>
</template>

<style scoped>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #f5f7fa;
    color: #1f2937;
}

.workspace-header h1 {
    margin: 5px 0 0;
    font-size: 28px;
}

.workspace-header__members {
    padding: 10px 16px;
    background: white;
    border-radius: 8px;
}

.workspace__content {
    display: grid;
    grid-template-columns: 1fr 280px;
    gap: 24px;
}

.projects,
.team-info {
    background: white;
    border-radius: 12px;
    padding: 24px;
}

.projects__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}

.projects__header h2,
.team-info h2 {
    margin: 0;
}

.projects__header p {
    margin: 6px 0 0;
    color: #6b7280;
}

.projects__counter {
    font-size: 14px;
    color: #6b7280;
}

.projects__list {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 16px;
}

.team-info ul {
    padding: 0;
    margin: 20px 0 0;
    list-style: none;
}

.team-info li {
    padding: 12px 0;
    border-bottom: 1px solid #e5e7eb;
}
</style>
<script setup>
import noData from './noData.vue';
const props = defineProps(["viewingProjectData"])
</script>
<template>

    <noData v-if="props.viewingProjectData.length == 0"></noData>
    <!-- {{ props.viewingProjectData }} -->
    <div class="" v-for="item in props.viewingProjectData" :key="item.id">
        <h1 class="SectionTitle text-white text-center">{{ item.fullName }} Projects</h1>
        <ul class="lists mx-4" v-for="project in item.projects" :key="project.id">
            <li class="bg-light text-dark fw-bold">{{ project.title }}</li>
        </ul>
    </div>
</template>

<style scoped></style>

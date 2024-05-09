<script setup>

import { RouterView } from 'vue-router'
import Navbar from '@/components/Navbar.vue'

</script>

<template>
    <!--
    <header v-if="!['Home'].includes($route.name)">
        <Navbar v-if="!['Home'].includes($route.name)" />
    </header>
    -->
    <header v-if="!['Home'].includes($route.name)">
        <Navbar />
    </header>

    <main>
        <RouterView />
    </main>

</template>

<style scoped>
header{
    display: inline-block;
    vertical-align: top;
    height: auto;
    width: 100%;
}

</style>


<script setup>
import { RouterLink } from 'vue-router'
</script>
<template>
    <div class="sidebar">
        <ul>
            <li><RouterLink to="/"><i class='bx bx-movie-play'></i>My Recordings</RouterLink></li>
            <li><a href="#"><i class='bx bx-share-alt'></i>Requested</a></li>
        </ul>
    </div>
    </template>
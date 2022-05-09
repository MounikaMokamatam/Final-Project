<script setup lang="ts">

import { useSession } from "../models/session";
const session = useSession();
</script>

<template>
    <div class="section homePagebg">
        <h1 v-if="!session.user" class="title">Welcome, This is the login page</h1>
        <h1 v-else class="title">Welcome, {{session.user.firstName}} {{session.user.firstName}}</h1> 
    </div>
</template>

<style scoped>
.title{
    text-align: center;
}
</style>
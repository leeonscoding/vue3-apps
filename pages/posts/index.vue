<script setup lang="ts">
    interface Post {
        title: string;
        body: string;
    }

    const url = 'https://jsonplaceholder.typicode.com/posts?_start=5&_limit=10'
    const requestObject = {
        query: {
            _start: 1,
            _limit: 5
        }
    }

    const { data, status, error, refresh } = useFetch<Post[]>(url, requestObject)

</script>

<template>
    <v-container>
        <v-row>
            <v-col>
                <h1>jsonplaceholder posts</h1>
            </v-col>
            <v-col>
                <v-btn @click="refresh()">Refresh</v-btn>
            </v-col>
        </v-row>

        <v-row v-if="error">
            <v-alert>{{ error.message }}</v-alert>
        </v-row>

        <v-sheet class="d-flex flex-wrap mx-auto pa-md-4 ma-md-4" elevation="4" width="100%" rounded
            v-for="obj in data">
            <h2>{{ obj.title }}</h2>
            <p>{{ obj.body }}</p>
        </v-sheet>
    </v-container>

</template>
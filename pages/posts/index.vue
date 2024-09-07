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
    const { data, status, error, refresh } = useFetch(url, requestObject)


</script>

<template>
    <v-container>
        <v-row>
            <v-col>
                <h1>Blog</h1>
            </v-col>
            <v-col>
                <v-btn @click="refresh()">Refresh</v-btn>
            </v-col>
        </v-row>

        <v-row v-if="error">
            <v-alert>{{ error.message }}</v-alert>
        </v-row>

        <v-row v-for="obj in data">
            <v-card class="pa-md-4 ma-md-4">
                <v-card-title>{{ obj.title }}</v-card-title>
                <v-card-text>{{ obj.body }}</v-card-text>
            </v-card>
        </v-row>
    </v-container>    

</template>
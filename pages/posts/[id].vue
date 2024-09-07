<script setup lang="ts">
    interface Post {
        id: number;
        title: string;
        body: string;
    }

    const urlParam = useRoute().params.id
    const url = `https://jsonplaceholder.typicode.com/posts/${urlParam}`
    const { data, status, error, refresh } = useFetch<Post>(url)


</script>

<template>
    <v-container>
        <v-row v-if="error">
            <v-alert>{{ error.message }}</v-alert>
        </v-row>

        <div v-else>
            <v-row>
                <h2>{{ data?.title }}</h2>
            </v-row>

            <v-row>
                <p>{{ data?.body }}</p>
            </v-row>
        </div>
    </v-container>
</template>
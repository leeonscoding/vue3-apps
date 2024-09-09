<script setup lang="ts">
    interface Post {
        id: number;
        title: string;
        body: string;
    }

    const totalCount = ref<number>(0)

    const baseUrl = 'https://jsonplaceholder.typicode.com/posts'
    const countHeaderString = 'x-total-count'

    const result = ref<Post[]|null|undefined>();

    const itemPerPage = 5;
    const pageNo = ref(0)

    const { data,
        status,
        error,
        refresh } = await useFetch<Post[]>(baseUrl, {
            onRequest({ request, options }) {
                options.query = {
                    _start: 0,
                    _limit: itemPerPage
                }
            },
            onResponse({ response }) {
                const getCount = response.headers.get(countHeaderString)

                if(getCount) totalCount.value = Number.parseInt(getCount)
            }
        })

    result.value = data.value
    const totalPage = ref(totalCount.value / itemPerPage)

    watch(pageNo, async(newPageNo) => {
        const requestObject1 = {
            query: {
                _start: newPageNo,
                _limit: itemPerPage
            }
        }

        const data  = await $fetch<Post[]>(baseUrl, requestObject1)
        result.value = data
    })

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

        <v-row>
            <v-sheet class="pa-md-4 ma-md-4 ga-3" elevation="4" width="100%" rounded
                v-for="obj in result">
                <NuxtLink :to="{path: `/posts/${obj.id}`}" class="text-decoration-none">
                    <h2>{{ obj.title }}</h2>
                    <p>{{ obj.body.substring(0, 20) }}</p>
                </NuxtLink>
            </v-sheet>
        </v-row>

        <v-row>
            <v-pagination
                v-model="pageNo"
                :length="totalPage"
                rounded="circle"
            ></v-pagination>
        </v-row>
    </v-container>

</template>
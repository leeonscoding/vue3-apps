<script setup lang="ts">
    const items = [
        {
            title: 'page1',
            value: 'page1Link',
            icon: 'mdi-account'
        },
        {
            title: 'page2',
            value: 'page2Link',
            icon: 'mdi-account'
        },
    ]
    const drawer = ref(false)
    const group = ref(null)

    watch(group, () => {
        drawer.value = false
    })
</script>

<template>
    <v-app>
        <v-app-bar color="primary" :elevation="2">
            <template v-slot:prepend>
                <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
            </template>

            <v-app-bar-title>Simple projects</v-app-bar-title>

            <v-spacer></v-spacer>

            <v-btn icon>
            <v-icon>mdi-magnify</v-icon>
            </v-btn>

            <v-btn icon>
            <v-icon>mdi-heart</v-icon>
            </v-btn>

            <template v-slot:append>
                <v-btn icon="mdi-dots-vertical"></v-btn>
            </template>
        </v-app-bar>

        <v-navigation-drawer
            v-model="drawer"
            :location="$vuetify.display.mobile ? 'bottom' : undefined"
            temporary
        >
            <v-list nav>
                <v-list-item v-for="item in items"
                    :prepend-icon="item.icon"
                    :title="item.title"
                ></v-list-item>
            </v-list>
        </v-navigation-drawer>

        <v-main>
            <slot />
        </v-main>
    </v-app>
</template>
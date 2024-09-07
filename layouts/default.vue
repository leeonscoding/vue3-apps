<template>
    <v-app>
        <v-app-bar color="primary" :elevation="2">
            <template v-slot:prepend>
                <v-app-bar-nav-icon></v-app-bar-nav-icon>
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
        <v-main>
            <slot />
        </v-main>
    </v-app>
</template>
<template>
  <div>
    <v-app id="inspire">
      <v-app-bar>
        <v-app-bar-nav-icon></v-app-bar-nav-icon>
        <v-app-bar-title>Customer List</v-app-bar-title>
        <v-spacer></v-spacer>
      </v-app-bar>
      <v-main>
        <slot />
      </v-main>
    </v-app>
  </div>
</template>
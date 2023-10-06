
<template>
    <v-app id="inspire">
    <v-app-bar>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-app-bar-title>Customer List (show all: {{ show_all_model_text }})</v-app-bar-title>

      <v-spacer></v-spacer>

      <div class="switch-container">
            <v-switch color="primary" v-model="show_all_model" density="dense" messages="show all"></v-switch>
      </div>
    </v-app-bar>

    <v-main>
      <Users :show_all="show_all_model"></Users>
    </v-main>
  </v-app>
</template>

<script setup>
const show_all_model = ref(false);
const show_all_model_text = computed(() => show_all_model.value ? "yes" : "no");
</script>

<style scoped>
.switch-container {
  margin: 5px; 
  height: 100%;
  display:flex;
  justify-content:center;
  align-items:center; 
  height: 100%;
}

.footer {
  width: 100%;
  text-align: center;
  bottom: 2em;
  color: aliceblue;
}
</style>
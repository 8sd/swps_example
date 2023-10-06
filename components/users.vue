<script setup>
const props = defineProps({
  show_all: Boolean
})
const { data: users, pending, error } = await useFetch(`http://localhost:8080/v1/graphql`, {
  method: "POST", 
  body: { query: "query { swps_Personen { Vorname Name Mail Anrede Aktiv Personen_ID PersonenExt { Latest_update PIN Personen_ID } } }" },
})
</script>

<template>
    <p v-if="pending">Fetching...</p>
    <pre v-else-if="error">Could not load: {{ error.data }}</pre>
    <div v-else>
      <v-container>
        <v-row>
          <v-col
            v-for="user in users.data.swps_Personen"
            :key="user.Personen_ID"
            sm="4"
          >
            <User :user="user" v-if="props.show_all || user.Aktiv"></User>
          </v-col>
        </v-row>
      </v-container>
    </div>
</template>

<style scoped>
</style>
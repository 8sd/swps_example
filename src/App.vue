<template>
  <v-app>
    <v-container>
      <!-- Conditional Rendering: Show LoginPage if not authenticated, else show MapComponent -->
      <LoginPage v-if="!isAuthenticated" @login="handleLogin" />
      <MapComponent v-if="isAuthenticated" :userName="userName" :userPassword="userPassword" />
    </v-container>
  </v-app>
</template>

<script>
import LoginPage from './components/LoginPage.vue';
import MapComponent from './components/MapComponent.vue';

export default {
  data() {
    return {
      isAuthenticated: false, // Initially set to false, user is not logged in
      userName: '', // Store the user's name here
    };
  },
  components: {
    LoginPage,
    MapComponent,
  },
  methods: {
    handleLogin({ name, password }) {
      // Hardcoded password check
      if (password === 'eyJhbGci') {
        this.userName = name; // Store the user's name when login is successful
        this.userPassword = password;
        this.isAuthenticated = true; // Set authentication flag to true
      } else {
        alert('Incorrect password. Please try again.');
      }
    },
  },
};
</script>

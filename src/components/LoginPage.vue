<template>
  <v-container>
    <v-row justify="center" align="center" style="height: 100vh">
      <v-col cols="12" md="4">
        <v-card class="pa-4" elevation="2">
          <v-card-title class="title text-center">
            Login
          </v-card-title>

          <v-card-text>
            <v-form v-model="valid">
              <v-text-field
                v-model="name"
                label="Name"
                required
              ></v-text-field>

              <v-text-field
                v-model="password"
                label="Password"
                type="password"
                required
              ></v-text-field>

              <v-btn
                :disabled="!valid"
                color="primary"
                block
                @click="submitLogin"
              >
                Login
              </v-btn>

              <v-alert v-if="errorMessage" type="error" class="mt-3">
                {{ errorMessage }}
              </v-alert>
            </v-form>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      name: '', // Store the user's name
      password: '', // Store the user's password
      valid: true,
      errorMessage: '',
    };
  },
  methods: {
    submitLogin() {
      if (this.password !== 'eyJhbGci') {
        this.errorMessage = 'Incorrect password. Please try again.';
      } else {
        this.$emit('login', { name: this.name, password: this.password }); // Emit both name and password
      }
    },
  },
};
</script>

<style scoped>
.title {
  font-weight: bold;
  color: #333;
}
</style>

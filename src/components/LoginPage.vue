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
import { createClient } from '@supabase/supabase-js';

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
    async submitLogin() {
      const supabaseUrl = 'https://ldpsaujnvjyjtflecpgb.supabase.co';
      const supabaseKey = this.password + 'OiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImxkcHNhdWpudmp5anRmbGVjcGdiIiwicm9sZSI6ImFub24iLCJpYXQiOjE3MjU5NTc4NDcsImV4cCI6MjA0MTUzMzg0N30.56c2P7OPQyNd1flTA4vlyZ7Hn_8sFAWG8ThW6Q341DI';
      
      const supabase = createClient(supabaseUrl, supabaseKey);

      try {
        // Try fetching data from Supabase to verify if the password is correct
        const { data, error } = await supabase.from('orte').select('*').limit(1);
        
        if (error || !data) {
          this.errorMessage = 'Incorrect password. Please try again.';
        } else {
          // If the data is fetched successfully, emit the login event
          this.$emit('login', { name: this.name, password: this.password });
        }
      } catch (err) {
        this.errorMessage = 'Error connecting to Supabase. Please try again.';
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

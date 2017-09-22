<template>
  <v-container class="grey lighten-4 mb-2">
    <v-layout row>
      <v-flex xs12 sm6 offset-sm3>
        <v-card>
          <v-card-title>
            <div class="headline primary--text">Register</div>
          </v-card-title>
          <v-divider></v-divider>
          <v-card-text>
            <v-form v-model="valid" ref="form" @submit.prevent="onRegister">
              <v-layout row>
                <v-flex xs12>
                  <v-text-field 
                    type="email" 
                    name="email" 
                    label="Email" 
                    v-model="email" 
                    :rules="emailRules" 
                    required>
                  </v-text-field>
                </v-flex>
              </v-layout>
              <v-layout row>
                <v-flex xs12>
                  <v-text-field 
                    name="password" 
                    label="Password" 
                    v-model="password" 
                    type="password" 
                    :counter="6" 
                    :rules="passwordRules" 
                    required>
                  </v-text-field>
                </v-flex>
              </v-layout>
              <v-layout row class="mt-2">
                <v-flex xs12>
                  <v-btn class="primary" type="submit">Register</v-btn>
                </v-flex>
              </v-layout>
            </v-form>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  import AuthenticationService from '@/services/AuthenticationService'
  export default {
    data() {
      return {
        valid: false,
        email: '',
        emailRules: [
          (v) => !!v || 'E-mail is required',
          (v) => /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
        ],
        password: '',
        passwordRules: [
          (v) => v && v.length >= 6 || 'Password must be more than 6 characters'
        ]
      }
    },
    computed: {
    },
    watch: {
      user(value) {
        if (value !== null && value !== undefined) {
          this.$router.push('/')
        }
      }
    },
    methods: {
      async onRegister() {
        if (this.$refs.form.validate()) {
          await AuthenticationService.register({
            email: this.email,
            password: this.password
          })
        }
      },
      onDismissed () {
        this.$store.dispatch('clearError')
      }
    }
  }
</script>

<style scoped>
  
</style>

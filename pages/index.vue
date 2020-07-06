<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <div class="text-center">
        <logo />
      </div>
      <v-card>
        <v-card-title class="headline"
          >Welcome to Congratulations!</v-card-title
        >
        <v-card-text>
          <p>
            Get a list of people who congratulated you in your memorable days.
          </p>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <facebook-login
            @loggedIn="$router.push('schindler')"
          ></facebook-login>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo,
  },
}
</script>

<template>
  <div>
    <v-btn @click="logInWithFacebook">Get Started</v-btn>
  </div>
</template>
<script>
export default {
  name: 'FacebookLogin',
  data: () => ({
    disabled: true,
  }),
  methods: {
    logInWithFacebook() {
      const vm = this
      window.FB.login(
        function (response) {
          if (response.authResponse) {
            // Now you can redirect the user or do an AJAX request to
            // a PHP script that grabs the signed request from the cookie.
            vm.statusChangeCallback(response)
          } else {
          }
        },
        {
          scope: 'pages_read_engagement,pages_manage_metadata,pages_messaging',
        }
      )
      return false
    },
    statusChangeCallback(response) {
      this.$emit(
        'loggedIn',
        response.authResponse.accessToken,
        response.authResponse.userID
      )
    },
  },
}
</script>
<style>
.button {
  color: white;
  min-width: 150px;
  background-color: #000000a1;
  height: 2.5rem;
  border-radius: 2rem;
  font-weight: 400;
  font-size: 0.8rem;
}
</style>

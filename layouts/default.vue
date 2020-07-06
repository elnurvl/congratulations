<template>
  <v-app>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-img
        class="mx-2"
        src="logo.png"
        max-height="40"
        max-width="40"
        contain
      ></v-img>
      <nuxt-link style="text-decoration: none; color: inherit;" to="/">
        <v-toolbar-title v-text="title" />
      </nuxt-link>
    </v-app-bar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }} Elnur Hajiyev</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Congratulations',
    }
  },
  head() {
    return {
      title: 'Congratulations',
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: 'description',
          name: 'description',
          content: 'Get list of people who respects you',
        },
      ],
    }
  },
}
</script>

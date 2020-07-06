<template>
  <v-row justify="center">
    <v-dialog ref="dialog" v-model="dialog" width="600px">
      <v-card>
        <v-card-title>
          <span class="headline">List of names</span>
        </v-card-title>
        <v-card-text>
          <ol ref="list">
            <li v-for="(name, index) in names" :key="index">{{ name }}</li>
          </ol>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" text @click="copy">Copy</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-snackbar v-model="message">Copied!</v-snackbar>
  </v-row>
</template>

<script>
export default {
  name: 'List',
  props: {
    names: {
      type: Array,
      default() {
        return []
      },
    },
  },
  data: () => ({
    dialog: false,
    message: false,
  }),
  methods: {
    copy: function copy() {
      const instance = this
      this.$copyText(this.$refs.list.textContent).then(function (_) {
        instance.message = true
      })
    },
  },
}
</script>

<template>
  <v-container>
    <v-row>
      <v-col>
        <h2>Choose a page</h2>
        <v-radio-group v-model="page_id" :mandatory="false">
          <v-radio
            v-for="page in pages"
            :key="page.id"
            :label="page.name"
            :value="page.id"
          ></v-radio>
        </v-radio-group>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <h2 v-if="hacker">From</h2>
        <h2 v-if="!hacker">Choose your memorable day</h2>
        <v-date-picker v-model="birthday"></v-date-picker>
      </v-col>
      <v-col v-if="hacker">
        <h2>To</h2>
        <v-date-picker v-model="toDate"></v-date-picker>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-switch v-model="hacker" label="Hacker Mode"></v-switch>
      </v-col>
    </v-row>
    <v-row v-if="hacker">
      <v-col>
        <v-combobox
          v-model="rules"
          label="Which words are you looking for?"
          multiple
          chips
          append-icon=""
        ></v-combobox>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-btn
          color="success"
          :disabled="page_access_token == null"
          @click="getMessages"
          >Get Names</v-btn
        >
      </v-col>
    </v-row>
    <list ref="list" :names="names"></list>
    <v-snackbar v-model="message">Copied!</v-snackbar>
    <v-snackbar v-model="hackerMessage"
      >Congratulations! Now you are a hacker! (Because it is dark)</v-snackbar
    >
    <v-overlay :value="loading">
      <v-progress-circular indeterminate size="64"></v-progress-circular>
    </v-overlay>
  </v-container>
</template>

<script>
import file from '@/assets/words.txt'
export default {
  data: () => ({
    userId: null,
    token: null,
    page_id: null,
    birthday: new Date().toISOString().substr(0, 10),
    toDate: new Date().toISOString().substr(0, 10),
    page_access_token: null,
    messages: [],
    pages: [],
    names: [],
    rules: [],
    message: false,
    loading: true,
    hacker: false,
    hackerMessage: false,
  }),
  watch: {
    page_id(_) {
      this.$axios
        .get(`/${this.page_id}`, {
          params: {
            fields: 'access_token',
            access_token: this.token,
          },
        })
        .then((res) => {
          this.page_access_token = res.data.access_token
        })
    },
    hacker(value) {
      if (value) {
        this.$nextTick(() => {
          this.$vuetify.theme.dark = true
          this.hackerMessage = true
        })
      }
      this.$vuetify.theme.dark = false
    },
  },
  async mounted() {
    const vm = this
    this.rules = file.split('\n').map((w) => w.trim())
    try {
      await window.FB.getLoginStatus(function (response) {
        vm.userId = response.authResponse.userID
        vm.token = response.authResponse.accessToken
      })
    } catch (_) {
      this.$router.push('/')
      return
    }
    await this.$axios
      .get(`/${this.userId}/accounts`, {
        params: {
          access_token: this.token,
        },
      })
      .then((response) => {
        this.pages = response.data.data
        if (this.pages.length === 1) {
          this.page_id = this.pages[0].id
        }
      })
    this.loading = false
  },
  methods: {
    async getMessages() {
      const vm = this
      await this.$axios
        .get(`/${this.page_id}`, {
          params: {
            fields: 'conversations{messages{message,created_time,from}}',
            access_token: this.page_access_token,
          },
        })
        .then((res) => {
          this.names = []
          this.messages = res.data
          const cons = res.data?.conversations?.data ?? []
          cons.forEach((con) => {
            const messages = con?.messages?.data ?? []
            messages.some((m) => {
              const text = m.message.toLowerCase()
              const id = m.from.id
              const created = m.created_time
              if (
                this.$moment(created).isBetween(
                  this.birthday,
                  this.hacker ? this.toDate : this.birthday,
                  'day',
                  '[]'
                ) &&
                id !== this.page_id &&
                this.rules.some((v) => text.includes(v))
              ) {
                this.names.push(m.from.name)
                return true
              }
            })
          })
          this.$copyText(
            this.names.map((n, i) => `${i + 1}. ${n}`).join('\n')
          ).then(function (_) {
            vm.message = true
          })
          this.$refs.list.dialog = true
        })
    },
  },
}
</script>

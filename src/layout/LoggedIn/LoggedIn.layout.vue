<template>
  <div>
    <logged-in-header
      :langs="langs"
      :lang="lang"
      @onChangeLanguage="changeLang"
    />
    <router-view />
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

import LoggedInHeader from '@/components/LoggedIn/header/header.component.vue'
import { langActions } from '@/store/lang/lang.actionTypes'

export default {
  name: 'LoggedInLayout',
  components: { LoggedInHeader },
  computed: {
    ...mapGetters({
      lang: 'lang',
      langs: 'langs',
    }),
  },
  methods: {
    ...mapActions({
      changeLanguage: langActions.CHANGE_LANGUAGE,
    }),
    changeLang(lang) {
      if (lang !== this.lang) {
        this.changeLanguage(lang).then(() => {
          return this.$router.push({ query: { ...this.$route.query, lang } })
        })
      }
    },
  },
}
</script>

<style scoped></style>

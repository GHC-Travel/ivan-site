<template>
  <v-app light>
    <v-app-bar :clipped-left="true" fixed app>
      <v-toolbar-title v-text="title" />
      <v-spacer />
      <v-btn text v-for="(link, index) in links" :key="index" nuxt :to="link.to" router exact>
        <v-icon>{{ link.icon }}</v-icon>
        {{ link.title }}
      </v-btn>

      <v-btn
        v-for="locale in availableLocales"
        :key="locale.code"
        nuxt
        text
        :to="switchLocalePath(locale.code)"
      >
        <component :is="locale.icon" width="15px" height="15px" />
      </v-btn>
    </v-app-bar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer fixed app>
      <span>&copy; {{ year }}</span>
    </v-footer>
  </v-app>
</template>

<script>
import { format } from 'date-fns'

export default {
  components: {
    da: () => import('~/components/Flags/Da'),
    en: () => import('~/components/Flags/En')
  },

  data: () => ({
    links: [
      {
        icon: 'mdi-home',
        title: 'Welcome',
        to: '/'
      },
      {
        icon: 'mdi-at',
        title: 'Contact',
        to: '/contact'
      }
    ],

    title: 'Ivans site'
  }),

  computed: {
    year() {
      return format(new Date(), 'Y')
    },

    availableLocales() {
      return this.$i18n.locales.filter(i => i.code !== this.$i18n.locale)
    }
  }
}
</script>

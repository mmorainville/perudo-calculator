<template>
  <div class="hero-head">
    <header class="nav">
      <div class="container">
        <div class="nav-left">
          <nuxt-link class="nav-item" :to="path('/')">
            Perudo Calculator
          </nuxt-link>
        </div>
        <span class="nav-toggle" @click="isMenuOpened = !isMenuOpened">
          <span></span>
          <span></span>
          <span></span>
        </span>
        <div class="nav-right nav-menu" :class="{ 'is-active': isMenuOpened }">
          <nuxt-link class="nav-item" :to="path('/')" exact>
            Accueil
          </nuxt-link>
          <nuxt-link class="nav-item" :to="path('/documentation')" exact>
            Documentation
          </nuxt-link>
          <a href="https://github.com/mmorainville/perudo-calculator" class="nav-item">
            GitHub
          </a>

          <span class="nav-item" v-if="$i18n.locale === 'en'">
            <nuxt-link class="button is-info is-inverted" :to="`/fr` + $route.fullPath" active-class="none" exact>FR</nuxt-link>
          </span>
          <span class="nav-item" v-if="$i18n.locale === 'fr'">
            <nuxt-link class="button is-info is-inverted" :to="$route.fullPath.replace(/^\/[^\/]+/, '')" active-class="none" exact>EN</nuxt-link>
          </span>
        </div>
      </div>
    </header>
  </div>
</template>

<script>
  export default {
    name: 'navbar',
    data () {
      return {
        isMenuOpened: false
      }
    },
    methods: {
      path (url) {
        return (this.$i18n.locale === 'en' ? url : '/' + this.$i18n.locale + url)
      }
    }
  }
</script>

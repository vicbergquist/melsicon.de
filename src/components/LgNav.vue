<template>
    <div class="nav">
        <div class="lg-nav-wrapper">
            <scrollactive
                v-if="$route.name === 'home'"
                :offset="0"
                :modify-url="false"
                class="lg-nav"
                role="navigation">
                <a
                    v-for="(nav, key) in $t('nav')"
                    :class="{'scrollactive-item': $route.name === 'home'}"
                    :href="'#' + key"
                    :key="nav.index"
                    class="nav-link">{{ nav }}</a>
                <button
                    class="locale-btn nav-link"
                    @click="toggleLocale">{{ locale }}</button>
            </scrollactive>
            <nav
                v-if="$route.name === 'imprint' || $route.name === 'privacy'"
                class="lg-nav"
                role="navigation">
                <router-link
                    :class="{'is-active': $route.name === 'home'}"
                    to="/"
                    class="nav-link">{{ $t('nav.home') }}</router-link>
                <router-link
                    :class="{'is-active': $route.name === 'imprint'}"
                    to="/imprint"
                    class="nav-link">{{ $t('footer.legal.imprint') }}</router-link>
                <button
                    class="locale-btn nav-link"
                    @click="toggleLocale">{{ locale }}</button>
            </nav>
            <the-logo/>
        </div>
    </div>
</template>

<script>
import TheLogo from '@/components/TheLogo'
export default {
  name: 'Navigation',
  components: {
    TheLogo
  },
  data: () => ({
    open: false
  }),
  computed: {
    locale() {
      if (this.$i18n.locale === 'de') {
        return 'English'
      } else {
        return 'Deutsch'
      }
    }
  },
  methods: {
    toggleLocale() {
      if (this.$i18n.locale === 'de') {
        this.$i18n.locale = 'en'
      } else {
        this.$i18n.locale = 'de'
      }
    }
  }
}
</script>

<style lang="sass" scoped>

  .nav
    position: fixed
    top: 0
    display: flex
    width: 100%
    background: white
    z-index: 9999
    margin: 0 auto

  .lg-nav-wrapper
    display: flex
    position: relative
    width: 100%
    max-width: $normal-width
    margin: auto
    padding: .5rem 1em
    align-items: center
    @include x-large
      max-width: $large-width

  .lg-nav
    display: flex
    width: 100%

  .logo
    fill: $color-primary
    margin-left: auto

  .nav-list
    display: flex
    width: 100%

  .nav-link, .locale-btn
    margin-right: 5%
    color: $color-black
    font-size: .9em
    letter-spacing: .5px
    text-decoration: none
    text-transform: uppercase
    transition: transform .3s ease-in
    border-bottom: 1px solid $color-white
    transition: all .3s ease-in

  .locale-btn
    cursor: pointer
    color: $color-black
    font-size: .83em
    &:active
      font-weight: 600
      color: $color-primary

  .is-active
    color: $color-primary
    font-weight: 600

</style>

<template>
  <div id="app">

    <header class="header">
      <div class="header__left">
        <Logo v-if="showLogo" /> 
      </div>
      
      <div class="header__right">        
        <ToggleTheme />
      </div>
    </header>

    <main class="main">
      <slot/>
    </main>

    <footer class="footer">
      <span class="footer__copyright"><strong>Museo Municipal de Guayaquil</strong> © {{ new Date().getFullYear() }}.</span>
      <span class="footer__copyright">Sucre entre Chile y Pedro Carbo. <strong>Tel. 04 259 4800</strong> ext. 7402 </span>
      <span class="footer__links">Powered by <a href="//gridsome.org"> Gridsome </a></span>
    </footer>

  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import ToggleTheme from '~/components/ToggleTheme.vue'

export default {
  props: {
    showLogo: { default: true }
  },
  components: {
    Logo,
    ToggleTheme
  }
}
</script>

<style lang="scss">
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  min-height: var(--header-height);
  padding: 0 calc(var(--space) / 2);
  top:0;
  z-index: 10;

  &__left,
  &__right {
    display: flex;
    align-items: center;
  }

  @media screen and (min-width: 1300px) {
    //Make header sticky for large screens
    position: sticky;
    width: 100%;
  }
}

.main {
  margin: 0 auto;
  padding: 1.5vw 15px 0;
}

.footer {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction:column;
  padding: calc(var(--space) / 2);
  text-align: center;
  font-size: .8em;

  > span {
    margin: 0 .35em;
  }

  a {
    color: currentColor;
  }
}
</style>

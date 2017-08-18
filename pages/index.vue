<template>
  <section class="hero is-info is-fullheight">
    <!-- Hero header: will stick at the top -->
    <div class="hero-head">
      <header class="nav">
        <div class="container">
          <div class="nav-left">
            <a class="nav-item">
              Perudo Calculator
            </a>
          </div>
          <span class="nav-toggle">
            <span></span>
            <span></span>
            <span></span>
          </span>
          <div class="nav-right nav-menu">
            <a class="nav-item is-active">
              Home
            </a>
            <a class="nav-item">
              Examples
            </a>
            <a class="nav-item">
              Documentation
            </a>
            <span class="nav-item">
              <a class="button is-success is-inverted">
                <span class="icon">
                  <i class="fa fa-github"></i>
                </span>
                <span>Download</span>
              </a>
            </span>
          </div>
        </div>
      </header>
    </div>

    <!-- Hero content: will be in the middle -->
    <div class="hero-body">
      <div class="container has-text-centered">
        <h1 class="title">
          Parmis <input class="c-input-number c-input-number--title" type="number" placeholder="n"> dés, il y a
        </h1>
        <h2 class="subtitle">
          (en règles normales)
        </h2>

        <div class="level">
          <div class="level-item has-text-centered">
            <div>
              <p class="heading">
                exactement <input class="c-input-number c-input-number--heading" type="number" placeholder="k">
                fois le nombre <input class="c-input-number c-input-number--heading" type="number" placeholder="x">
                ou le paco
              </p>
              <p class="title">3,456</p>
            </div>
          </div>
          <div class="level-item has-text-centered">
            <div>
              <p class="heading">au moins k fois le nombre l ou le paco</p>
              <p class="title">123</p>
            </div>
          </div>
        </div>

        <div class="level">
          <div class="level-item has-text-centered">
            <div>
              <p class="heading">exactement k fois le paco</p>
              <p class="title">456K</p>
            </div>
          </div>
          <div class="level-item has-text-centered">
            <div>
              <p class="heading">au moins k fois le paco</p>
              <p class="title">789</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Hero footer: will stick at the bottom -->
    <div class="hero-foot">
      <nav class="tabs is-boxed is-fullwidth">
        <div class="container">
          <ul>
            <li class="is-active"><a>Overview</a></li>
            <li><a>Modifiers</a></li>
            <li><a>Grid</a></li>
            <li><a>Elements</a></li>
            <li><a>Components</a></li>
            <li><a>Layout</a></li>
          </ul>
        </div>
      </nav>
    </div>
  </section>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  }
}
</script>

<style lang="scss">
.c-input-number {
  background: transparentize(white, 0.9);
  border: none;
  text-align: left;
  padding-left: 16px;
  color: white;
  font-weight: 600;

  &::placeholder {
    color: white;
  }

  &--title {
    line-height: 1.125;
    font-size: 2rem;
    width: 64px;
  }

  &--heading {
    font-size: 1rem;
    width: 48px;
  }
}
</style>

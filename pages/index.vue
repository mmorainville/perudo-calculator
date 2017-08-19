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
              Accueil
            </a>
            <a class="nav-item">
              Exemples
            </a>
            <a class="nav-item">
              Documentation
            </a>
          </div>
        </div>
      </header>
    </div>

    <!-- Hero content: will be in the middle -->
    <div class="hero-body">
      <div class="container has-text-centered">
        <h1 class="title">
          Parmi <input v-model.number="n" class="c-input-number c-input-number--title" type="number" placeholder="n" :min="k" step="1"> dés, il y a
        </h1>
        <h2 class="subtitle">
          (en règles normales)
        </h2>

        <div class="tile is-ancestor c-values">
          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block c-values__block--primary">
              <p class="heading">
                exactement <input v-model.number="k" class="c-input-number c-input-number--heading" type="number" placeholder="k" min="0" :max="n" step="1">
                fois le nombre <input v-model.number="l" class="c-input-number c-input-number--heading" type="number" placeholder="x" min="2" max="6">
                ou le paco
              </p>
              <p class="title">{{ Pankl | percentage }}</p>
            </div>
          </div>

          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block c-values__block--primary">
              <p class="heading">au moins {{ k }} fois le nombre {{ l || 'x' }} ou le paco</p>
              <p class="title">{{ PAnkl | percentage }}</p>
            </div>
          </div>

          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block c-values__block--primary">
              <p class="heading">exactement k fois le paco</p>
              <p class="title">{{ Pankpaco | percentage }}</p>
            </div>
          </div>

          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block c-values__block--primary">
              <p class="heading">au moins k fois le paco</p>
              <p class="title">{{ PAnkpaco | percentage }}</p>
            </div>
          </div>
        </div>

        <h1 class="title">
          Parmis mes <input v-model.number="m" class="c-input-number c-input-number--title" type="number" placeholder="m" min="1" :max="n > 5 ? 5 : n">
          dés, j'ai exactement <input v-model.number="j" class="c-input-number c-input-number--title" type="number" placeholder="j" min="0" :max="m">
          fois le nombre <input v-model.number="l" class="c-input-number c-input-number--title" type="number" placeholder="x" min="2" max="6">
          ou le paco
        </h1>
        <h2 class="subtitle">
          alors, parmi {{ n || 'n' }} dés, il y a
        </h2>

        <div class="tile is-ancestor c-values">
          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block c-values__block--primary">
              <p class="heading">
                exactement <input v-model.number="k" class="c-input-number c-input-number--heading" type="number" placeholder="k" min="0" :max="n" step="1">
                fois le nombre <input v-model.number="l" class="c-input-number c-input-number--heading" type="number" placeholder="x" min="2" max="6">
                ou le paco
              </p>
              <p class="title">{{ Pankl_mjl | percentage }}</p>
            </div>
          </div>

          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block c-values__block--primary">
              <p class="heading">au moins {{ k }} fois le nombre {{ l || 'x' }} ou le paco</p>
              <p class="title">{{ PAnkl_mjl | percentage }}</p>
            </div>
          </div>

          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block c-values__block--primary">
              <p class="heading">exactement k fois le paco</p>
              <p class="title">{{ Pankpaco_mjpaco | percentage }}</p>
            </div>
          </div>

          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block c-values__block--primary">
              <p class="heading">au moins k fois le paco</p>
              <p class="title">{{ PAnkpaco_mjpaco | percentage }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
  import math from 'mathjs'
  import Logo from '~/components/Logo.vue'

  if (process.browser) {
    window.math = math
  }

  export default {
    components: {
      Logo
    },
    data () {
      return {
        n: null,
        k: null,
        l: null,
        m: null,
        j: null
      }
    },
    computed: {
      // Parmis n dés, il y a exactement k fois le nombre l ou le paco
      Pankl () {
        return this.getExactly(this.n, this.k)
      },
      // Parmis n dés, il y a au moins k fois le nombre l ou le paco
      PAnkl () {
        return this.getAtLeast(this.n, this.k)
      },
      // Parmis n dés, il y a exactement k fois le paco
      Pankpaco () {
        return this.getExactly(this.n, this.k, true)
      },
      // Parmis n dés, il y a au moins k fois le paco
      PAnkpaco () {
        return this.getAtLeast(this.n, this.k, true)
      },
      Pankl_mjl () {
        return this.getExactly(this.n - this.m, this.k - this.j)
      },
      // Parmis n dés, il y a au moins k fois le nombre l ou le paco
      PAnkl_mjl () {
        return this.getAtLeast(this.n - this.m, this.k - this.j)
      },
      // Parmis n dés, il y a exactement k fois le paco
      Pankpaco_mjpaco () {
        return this.getExactly(this.n - this.m, this.k - this.j, true)
      },
      // Parmis n dés, il y a au moins k fois le paco
      PAnkpaco_mjpaco () {
        return this.getAtLeast(this.n - this.m, this.k - this.j, true)
      }
    },
    methods: {
      getExactly (n, k, isPalifico) {
        let numerator = isPalifico ? 5 : 2
        let denominator = isPalifico ? 6 : 3
        try {
          return math.eval(`${math.combinations(n, k)} * ((${numerator} ^ (${n} - ${k})) / (${denominator} ^ ${n}))`)
        } catch (error) { console.warn(error) }
      },
      getAtLeast (n, k, isPalifico) {
        let numerator = isPalifico ? 5 : 2
        let denominator = isPalifico ? 6 : 3
        try {
          let result = null
          for (let i = 0; i < n - k + 1; i++) {
            result += math.eval(`${math.combinations(n, i + k)} * ((${numerator} ^ (${n} - ${i + k})) / (${denominator} ^ ${n}))`)
          }
          return result
        } catch (error) { console.warn(error) }
      }
    },
    filters: {
      percentage (value) {
        try {
          return math.format(math.eval(`${value} * 100`), {notation: 'fixed', precision: 2}) + ' %'
        } catch (error) { console.warn(error) }
      }
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
      width: 68px;
    }

    &--heading {
      font-size: 1rem;
      width: 48px;
    }
  }

  .c-values {
    &__block {
      &--primary {
        background-color: transparentize(#00d1b2, 0.5);
      }
    }
  }
</style>

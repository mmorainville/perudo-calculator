<template>
  <section class="hero is-info is-fullheight">
    <!-- Hero header: will stick at the top -->
    <navbar></navbar>

    <!-- Hero content: will be in the middle -->
    <div class="hero-body">
      <div class="container has-text-centered">
        <i18n path="index.title" tag="h1" class="title">
          <input v-model.number="n" class="c-input-number c-input-number--title" type="number" placeholder="n" :min="k || 1" step="1">
        </i18n>
        <h2 class="subtitle">
          {{ $t('index.subtitle') }}
        </h2>

        <div class="tile is-ancestor c-values">
          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block" :class="getBoxBackgroundColor(Pankl)">
              <i18n path="index.Pankl" tag="p" class="heading">
                <input v-model.number="k" class="c-input-number c-input-number--heading" type="number" placeholder="k" min="0" :max="n" step="1">
              </i18n>
              <p class="title" :title="Pankl">{{ Pankl | percentage }}</p>
            </div>
          </div>

          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block" :class="getBoxBackgroundColor(PAnkl)">
              <i18n path="index.Pankl_sum" tag="p" class="heading">{{ k || 'k' }}</i18n>
              <p class="title" :title="PAnkl">{{ PAnkl | percentage }}</p>
            </div>
          </div>

          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block" :class="getBoxBackgroundColor(Pankpaco)">
              <i18n path="index.Pankpaco" tag="p" class="heading">{{ k || 'k' }}</i18n>
              <p class="title" :title="Pankpaco">{{ Pankpaco | percentage }}</p>
            </div>
          </div>

          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block" :class="getBoxBackgroundColor(PAnkpaco)">
              <i18n path="index.Pankpaco_sum" tag="p" class="heading">{{ k || 'k' }}</i18n>
              <p class="title" :title="PAnkpaco">{{ PAnkpaco | percentage }}</p>
            </div>
          </div>
        </div>

        <i18n path="index.titleConditional" tag="h1" class="title">
          <input v-model.number="m" class="c-input-number c-input-number--title" type="number" placeholder="m" min="1" :max="n > 5 ? 5 : n">
          <input v-model.number="j" class="c-input-number c-input-number--title" type="number" placeholder="j" min="0" :max="m">
        </i18n>
        <i18n path="index.subtitleConditional" tag="h1" class="subtitle">
          {{ n || 'n' }}
        </i18n>

        <div class="tile is-ancestor c-values">
          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block" :class="getBoxBackgroundColor(Pankl_mjl)">
              <i18n path="index.Pankl" tag="p" class="heading">
                <input v-model.number="k" class="c-input-number c-input-number--heading" type="number" placeholder="k" min="0" :max="n" step="1">
              </i18n>
              <p class="title" :title="Pankl_mjl">{{ Pankl_mjl | percentage }}</p>
            </div>
          </div>

          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block" :class="getBoxBackgroundColor(PAnkl_mjl)">
              <i18n path="index.Pankl_sum" tag="p" class="heading">{{ k || 'k' }}</i18n>
              <p class="title" :title="PAnkl_mjl">{{ PAnkl_mjl | percentage }}</p>
            </div>
          </div>

          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block" :class="getBoxBackgroundColor(Pankpaco_mjpaco)">
              <i18n path="index.Pankpaco" tag="p" class="heading">{{ k || 'k' }}</i18n>
              <p class="title" :title="Pankpaco_mjpaco">{{ Pankpaco_mjpaco | percentage }}</p>
            </div>
          </div>

          <div class="tile is-parent">
            <div class="tile is-child box is-shadowless has-text-white c-values__block" :class="getBoxBackgroundColor(PAnkpaco_mjpaco)">
              <i18n path="index.Pankpaco_sum" tag="p" class="heading">{{ k || 'k' }}</i18n>
              <p class="title" :title="PAnkpaco_mjpaco">{{ PAnkpaco_mjpaco | percentage }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
  import math from 'mathjs'
  import Navbar from '~/components/Navbar'

  if (process.browser) {
    window.math = math
  }

  export default {
    components: {
      Navbar
    },
    data () {
      return {
        n: null,
        k: null,
        m: null,
        j: null
      }
    },
    computed: {
      // Parmi n dés, il y a exactement k fois un nombre de 2 à 6 ou le paco
      Pankl () {
        return this.getExactly(this.n, this.k)
      },
      // Parmi n dés, il y a au moins k fois un nombre de 2 à 6 ou le paco
      PAnkl () {
        return this.getAtLeast(this.n, this.k)
      },
      // Parmi n dés, il y a exactement k fois le paco
      Pankpaco () {
        return this.getExactly(this.n, this.k, true)
      },
      // Parmi n dés, il y a au moins k fois le paco
      PAnkpaco () {
        return this.getAtLeast(this.n, this.k, true)
      },
      // Parmi n dés, il y a exactement k fois un nombre de 2 à 6 ou le paco, sachant que j'ai exactement j fois un nombre de 2 à 6 ou le paco parmi mes m dés
      Pankl_mjl () {
        return this.getExactly(this.n - this.m, this.k - this.j)
      },
      // Parmi n dés, il y a au moins k fois un nombre de 2 à 6 ou le paco, sachant que j'ai exactement j fois un nombre de 2 à 6 ou le paco parmi mes m dés
      PAnkl_mjl () {
        return this.getAtLeast(this.n - this.m, this.k - this.j)
      },
      // Parmi n dés, il y a exactement k fois le paco, sachant que j'ai exactement j fois un nombre de 2 à 6 ou le paco parmi mes m dés
      Pankpaco_mjpaco () {
        return this.getExactly(this.n - this.m, this.k - this.j, true)
      },
      // Parmi n dés, il y a au moins k fois le paco, sachant que j'ai exactement j fois un nombre de 2 à 6 ou le paco parmi mes m dés
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
      },
      getBoxBackgroundColor (value) {
        return {
          'c-values__block--success': value > 0.75,
          'c-values__block--primary': (value <= 0.75 && value > 0.5) || !value,
          'c-values__block--warning': value <= 0.5 && value > 0.25,
          'c-values__block--danger': value <= 0.25
        }
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
      background-color: transparent;

      &--success {
        background-color: transparentize(hsl(141, 71%, 48%), 0.2);
      }

      &--primary {
        background-color: transparentize(hsl(171, 100%, 41%), 0.2);
      }

      &--warning {
        background-color: transparentize(hsl(48, 100%, 67%), 0.2);
      }

      &--danger {
        background-color: transparentize(hsl(348, 100%, 61%), 0.2);
      }
    }
  }
</style>

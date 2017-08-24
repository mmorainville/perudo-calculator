<template>
  <div>
    <section class="hero is-info">
      <navbar></navbar>
    </section>

    <section class="section">
      <div class="container">
        <article v-if="displayWarning" class="message is-warning">
          <div class="message-header">
            <p>{{ $t('documentation.warning') }}</p>
            <button class="delete" aria-label="delete" @click="displayWarning = false"></button>
          </div>
          <div class="message-body" v-html="$t('documentation.warningMessage')"></div>
        </article>

        <div class="content">
          <h1>Documentation</h1>
          <p>Ce site permet de calculer les probabilités au Perudo. Cette page est un résumé de la source<sup><a href="#source-1">[1]</a></sup> qui m'a inspiré et aidé à le faire.</p>

          <h2>Notations</h2>
          <p>Probabilités générales</p>
          <ul>
            <li><em>n</em> : le nombre de dés en jeu au total</li>
            <li><em>l</em> : un nombre entier compris entre 2 et 6</li>
            <li><em>k</em> : un nombre entier compris entre 0 et n : il s’agira du nombre de dés que l’on parie</li>
            <li><em>a<sub>n,k,l</sub></em> : l’évènement « Parmi n dés, il y a exactement k fois le nombre l ou le paco »</li>
            <li><em>A<sub>n,k,l</sub></em> : l’évènement « Parmi n dés, il y a au moins k fois le nombre l ou le paco »</li>
            <li><em>a<sub>n,k,paco</sub></em> : l’évènement « Parmi n dés, il y a exactement k fois le paco »</li>
            <li><em>A<sub>n,k,paco</sub></em> : l’évènement « Parmi n dés, il y a au moins k fois le paco »</li>
          </ul>

          <p>Probabilités condtionnelles</p>
          <ul>
            <li><em>m</em> : le nombre de dés sous notre gobelet</li>
            <li><em>j</em> : un nombre entier compris entre 0 et m</li>
            <li><em>a<sub>m,j,l</sub></em> : l’évènement « Parmi mes m dés, j’ai exactement j fois le nombre l ou le paco »</li>
            <li><em>a<sub>m,j,paco</sub></em> : l’évènement « Parmi mes m dés, j’ai exactement j fois le paco »</li>
          </ul>

          <h2>Formules</h2>

          <!-- P(a_{n,k,l}) = \binom{n}{k}\frac{2^{n-k}}{3^{n}} -->
          <figure>
            <img src="~/assets/Pankl.svg">
            <figcaption>
              Parmi n dés, il y a exactement k fois un nombre de 2 à 6 ou le paco
            </figcaption>
          </figure>

          <!-- P(A_{n,k,l}) = \sum_{i=k}^{n}\binom{n}{i}\frac{2^{n-i}}{3^{n}} -->
          <figure>
            <img src="~/assets/Pankl_sum.svg">
            <figcaption>
              Parmi n dés, il y a au moins k fois un nombre de 2 à 6 ou le paco
            </figcaption>
          </figure>

          <!-- P(a_{n,k,paco}) = \binom{n}{k}\frac{5^{n-k}}{6^{n}} -->
          <figure>
            <img src="~/assets/Pankpaco.svg">
            <figcaption>
              Parmi n dés, il y a exactement k fois le paco (ou un nombre de 2 à 6 en Palifico)
            </figcaption>
          </figure>

          <!-- P(A_{n,k,paco}) = \sum_{i=k}^{n}\binom{n}{i}\frac{5^{n-i}}{6^{n}} -->
          <figure>
            <img src="~/assets/Pankpaco_sum.svg">
            <figcaption>
              Parmi n dés, il y a au moins k fois le paco (ou un nombre de 2 à 6 en Palifico)
            </figcaption>
          </figure>

          <hr>

          <h6>Notes et références</h6>
          <ol>
            <li><a href="http://tcerantola.free.fr/IMG/pdf/les_probabilites_du_perudo.pdf" id="source-1">http://tcerantola.free.fr/IMG/pdf/les_probabilites_du_perudo.pdf</a></li>
          </ol>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
  import Navbar from '~/components/Navbar'

  export default {
    components: {
      Navbar
    },
    data () {
      return {
        displayWarning: true
      }
    }
  }
</script>

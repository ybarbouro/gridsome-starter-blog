<template>
  <Layout :show-logo="true">
    <!-- Author intro -->
    <Author :show-title="true" />

    <!-- Falta list posts -->

    <div class="bottom">

    <img src="//res.cloudinary.com/magnvs/image/upload/v1522811906/temporary_timbbp.jpg"/>

    <h2>Museo Municipal de Guayaquil</h2>
    <p>El Museo Municipal tiene la misión de guardar y difundir la historia de la ciudad para fortalecer la identidad del “ser” guayaquileño.</p>
    <p>El principal atractivo del museo está en su exposición permanente que narra cronológicamente la historia de la ciudad y la recientemente inaugurada sala de historia natural “Hno. Agustín Mantilla Figueroa”; además el edificio es la sede del Salón de Julio - Fundación de Guayaquil y de la exposición anual del Festival de Artes al Aire Libre - FAAL, ambos eventos plenamente institucionalizados y de trascendencia internacional para las Artes Visuales.</p>
    <p>Las salas de exposiciones temporales y el Auditorio del museo, tienen el honor de ser los anfitriones de la ciudad donde se muestran interesantes manifestaciones artísticas, se realizan eventos culturales y conferencias de historia en general.</p>
    <p>Todas estas características y cualidades señaladas convierten a esta entidad en un importante núcleo para la difusión del arte y la cultura en beneficio de la ciudadanía en general, hecho que la ha posicionado entre conocidas entidades culturales y artistas de renombre tanto nacionales como extranjeros.</p>

    <h2>Indice</h2>

    <p v-for="post in $page.posts.edges">
      <g-link :to="post.node.path">
        {{ post.node.title }}
      </g-link>
    </p>
    <Pager :info="$page.posts.pageInfo"/>
    </div>

</Layout>
</template>

<page-query>
query Posts ($page: Int) {
  posts: allPost (perPage: 10, page: $page) @paginate {
    totalCount
    pageInfo {
     totalPages
     currentPage
     isFirst
     isLast
   }
    edges {
      node {
        id
        title
        path
        tags {
          id
          title
          path
        }
        date (format: "D. MMMM YYYY")
        timeToRead
        description
        coverImage (width: 770, height: 380, blur: 10)
        ...on Post {
            id
            title
            path
        }
      }
    }
  }
}
</page-query>

<script>
import Author from '~/components/Author.vue'
import PostCard from '~/components/PostCard.vue'
import { Pager } from 'gridsome'

export default {
  components: {
    Author,
    PostCard,
    Pager
  },
  metaInfo: {
    title: '¡Comunicando!'
  }
}

</script>

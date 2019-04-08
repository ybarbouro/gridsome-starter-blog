<template>
  <Layout :show-logo="false">
    <!-- Author intro -->
    <Author :show-title="true" />

    <!-- List posts -->

    <div class="posts">
      <PostCard v-for="edge in $page.posts.edges" :key="edge.node.id" :post="edge.node"/>
    </div>

    <div class="bottom">
    <h2>INDEX</h2>
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
  posts: allPost (perPage: 4, page: $page) @paginate {
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

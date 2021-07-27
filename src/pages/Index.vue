<template>
  <layout>

    <!-- Page Header -->
    <header class="masthead" :style="{backgroundImage: `url(http://localhost:1337${general.cover.url}`}">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{ general.title }}</h1>
              <span class="subheading">{{ general.subtitle }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto" v-for="edge in $page.posts.edges" :key="edge.node.id">
          <div class="post-preview">
            <g-link :to="'/post/' + edge.node.id">
              <h2 class="post-title">
                {{ edge.node.title }}
              </h2>
              <h3 class="post-subtitle">

              </h3>
            </g-link>
            <p class="post-meta">Posts by
              <a href="#">{{ edge.node.created_by.firstname + edge.node.created_by.lastname }}</a>
              {{ edge.node.created_at }}</p>
            <p>
              <g-link :to="'/tag/' + tag.id" v-for="tag in edge.node.tags" :key="tag.id">{{ tag.title }}</g-link>
            </p>
          </div>
          <!-- Pager -->

          <pager :info="$page.posts.pageInfo" />
          <hr />
        </div>
      </div>
    </div>

  </layout>
</template>

<page-query>
query ($page: Int) {
  posts: allStrapiPost (perPage: 1, page: $page) @paginate {
    pageInfo {
      totalPages,
      currentPage
    }
    edges {
      node {
        id
        title
        tags {
            id
            title
          }
        created_by {
            id
            firstname
            lastname
          }
        created_at
      }
    }
  }

  general: allStrapiGeneral {
    edges {
      node {
        id
        title
        subtitle
        cover {
          url
        }
      }
    }
  }
}
</page-query>

<script>
import { Pager } from 'gridsome'

export default {
  name: 'HomePage',
  metaInfo: {
    title: 'Hello, world!'
  },
  components: {
    Pager
  },
  computed: {
    general () {
      return this.$page.general.edges[0].node
    }
  }
}
</script>

<style>
nav a {
  display: inline-block;
  width: 50px;
}
</style>

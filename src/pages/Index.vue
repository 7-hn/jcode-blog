<template>
  <layout>

    <!-- Page Header -->
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>Clean Blog</h1>
              <span class="subheading">A Blog Theme by Start Bootstrap</span>
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
              <a href="#" v-for="name in edge.node.created_bies">{{ name.firstname + name.lastname }}</a>
              {{ edge.node.created_at }}</p>
            <p>
              <a href="#" v-for="tag in edge.node.tags" :key="tag.id">{{ tag.title }}</a>
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
        created_bies {
            id
            firstname
            lastname
          }
        created_at
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
  }
}
</script>

<style>
nav a {
  display: inline-block;
  width: 50px;
}
</style>

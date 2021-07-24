<template>
  <layout>
    <!-- Page Header -->
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>#{{ $page.tag.title }}</h1>
              <span class="subheading">A Blog Theme by Start Bootstrap</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto" v-for="edge in $page.tag.posts" :key="edge.id">
          <div class="post-preview">
            <g-link :to="'/post/' + edge.id">
              <h2 class="post-title">
                {{ edge.title }}
              </h2>
              <h3 class="post-subtitle">

              </h3>
            </g-link>
        </div>
      </div>
    </div>
    </div>
  </layout>
</template>
<page-query>
query ($id: ID!) {
  tag: strapiTag (id: $id) {
    id
    title
    posts {
      id
      title
    }
  }
}
</page-query>

<script>
export default {
  name: "Tag"
}
</script>

<style scoped>

</style>
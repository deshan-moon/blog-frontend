<template>
  <Layout>
    <!-- Page Header-->
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
            <h1> # {{$page.strapiTag.title }}</h1>
              <!-- <span class="subheading">A Blog Theme by Start Bootstrap</span> -->
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content-->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="post in $page.strapiTag.posts" :key="post.id">
            <g-link :to="'/post/' + post.id">
              <h2 class="post-title">{{ post.id +' '+ post.title }}</h2>
              <h3 class="post-subtitle">{{ post.content }}</h3>
            </g-link>
            <p class="post-meta">
              Posted by
              <a href="#!">{{ post.autor }}</a>
              <!-- on September 24, 2021  -->
              {{ post.updated_at }}
            </p>
            <hr />
          </div>
          <!-- Pager-->
          <div class="clearfix">
            <!-- <a class="btn btn-primary float-right" href="#!">Older Posts →</a> -->
            <!-- <Pager :info="$page.allStrapiPost.pageInfo" /> -->
          </div>
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query ($id:ID!) {
  strapiTag (id:$id){
    id
    title
    posts {
      id
      title
      author
      updated_at
      content
    }
  }
}
</page-query>

<script>
import MarkdownIt from "markdown-it";
const md = new MarkdownIt();
export default {
  metaInfo: {
    title: "Posts"
  },
  name: "PostPage",
  methods: {
    mdToHTML(markdown) {
      return md.render(markdown);
    }
  }
};
</script>

<template>
    <Layout>
        <!-- Page Header-->
        <header class="masthead" :style="{backgroundImage:`url(${GRIDSOME_API_URL + general.cover[0].url })` }">
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
        <!-- Main Content-->
        <div class="container">
            <div class="row">
                <div class="col-lg-8 col-md-10 mx-auto">
                    <div class="post-preview" v-for="edge in $page.allStrapiPost.edges" :key="edge.node.id">
                        <g-link :to="'/post/' + edge.node.id">
                            <h2 class="post-title">{{ edge.node.id +' '+ edge.node.title }}</h2>
                            <h3 class="post-subtitle">{{ edge.node.content }}</h3>
                        </g-link>
                        <p class="post-meta">
                            Posted by
                            <a href="#!">{{ edge.node.autor }}</a>
                            <!-- on September 24, 2021  -->
                            {{ edge.node.updated_at }}
                        </p>
                        <p>
                            <span v-for="tag in edge.node.tags" :key="tag.id">
                                <g-link :to="'/tag/' + tag.id"> {{ tag.title }} </g-link> &nbsp;&nbsp;
                            </span>
                        </p>
                        <hr />
                    </div>
                    <!-- Pager-->
                    <div class="clearfix">
                        <!-- <a class="btn btn-primary float-right" href="#!">Older Posts →</a> -->
                        <Pager :info="$page.allStrapiPost.pageInfo"/>
                    </div>
                </div>
            </div>
        </div>
        <!-- query { posts: allStrapiPost { edges { node { id title content author updated_at tags { id title } } } } } -->
    </Layout>

</template>

<page-query>
query ($page:Int) {
	allStrapiPost (perPage: 2, page: $page) @paginate {
        pageInfo {
            totalPages
            currentPage
        }
  	    edges {
            node {
                id
                title
                author
                updated_at
                tags {
                    id
                    title
                }
                content
            }
        }
	}
    allStrapiGeneral {
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
const moment = require("moment");
var createTime = "2019-11-08 12:08:09";

import { Pager } from "gridsome";

export default {
  metaInfo: {
    title: "Hello, world!"
  },
  name: "HomePage",
  created() {},
  components: {
    Pager
  },
  computed:{
    general(){
        return this.$page.allStrapiGeneral.edges[0].node
    }
  }
};
</script>

<style>
.home-links a {
  margin-right: 1rem;
}
</style>

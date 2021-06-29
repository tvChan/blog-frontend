<template>
  <Layout>
    <!-- Page Header -->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(${GRIDSOME_API_URL}${$page.post.cover.url})`
      }">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-heading">
              <h1>{{ $page.post.title }}</h1>
              <!-- <span class="meta">Posted by
                <a href="#">Start Bootstrap</a> -->
                on {{ $page.post.created_at }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Post Content -->
    <article>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto" v-html="mdToHtml($page.post.content)">
          </div>
        </div>
      </div>
    </article>
  </Layout>
</template>
<page-query>
query($id: ID!) {
  post: strapiPosts (id: $id) {
    id
    title
    content
    cover {
      url
    }
    created_at
    tags {
      id
      title
    }
  }
}
</page-query>
<script>
import MarkdownIt from 'markdown-it'
const md = new MarkdownIt()

export default {
  name: 'PostPage',
  methods: {
    mdToHtml(str) {
      return md.render(str)
    }
  }
}
</script>

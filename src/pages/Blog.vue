<template>
  <Layout>
    <section id="container-centre" class="column centre flex-1">
      <h1 class="page-title text-3xl md:text-center md:text-5xl mb-16 lg:mb-24 lg:text-6xl">Blog</h1>
      <div class="px-2">
        <div class="posts flex flex-wrap -mx-2">
          <div
            class="w-full md:w-1/3 mb-8 px-2"
            v-for="entry in $page.allBlog.edges"
            :key="entry.node.id"
          >
            <article class="article-card bg-white overflow-hidden rounded-lg shadow-lg flex-1">
              <g-link
                class="featured-image-link block relative overflow-hidden"
                :to="entry.node.path"
              >
                <figure>
                  <g-image
                    class="block loaded"
                    :alt="entry.node.image_caption"
                    :src="entry.node.cover_image"
                  />
                </figure>
              </g-link>
              <div class="p-8">
                <h2 class="text-2xl mb-6">
                  <g-link
                    class="block text-purple-900 hover:text-pink-500"
                    :to="entry.node.path"
                  >{{ entry.node.title }}</g-link>
                </h2>
                <div class="text-sm text-gray-600 md:flex mb-4">
                  <p class="author">{{ entry.node.author.name }}</p>
                  <p class="hidden md:block px-2">—</p>
                  <time :datetime="entry.node.datetime">{{ entry.node.humanTime }}</time>
                </div>
              </div>
              <div class="p-8 text-sm text-gray-600 md:flex mb-4">
                <ul class="flex">
                  <li class="mr-2" v-for="tag in entry.node.tags" :key="tag.id">
                    <g-link
                      :to="tag.path"
                      class="border border-pink-300 px-3 py-2 text-pink-500 text-sx font-semibold rounded hover:text-white hover:bg-pink-500 hover:border-pink-500"
                    >
                      {{ tag.title }}
                    </g-link>

                  </li>
                </ul>
              </div>
            </article>
          </div>
        </div>
      </div>
    </section>
  </Layout>
</template>

<script>
export default {
  metaInfo: {
    title: "Blog"
  }
};
</script>

<page-query>
  query {
    allBlog (order: DESC) {
      edges {
        node {
          title
          path
          cover_image(width:780)
          humanTime : date(format:"Do MMMM YYYY")
          datetime : date(format:"ddd MMM DD YYYY")
          author {
            name
          }
          tags {
                id
                title
                path
          }
        }
      }
    }
  }
</page-query>


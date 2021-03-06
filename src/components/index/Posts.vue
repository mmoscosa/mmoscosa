<template>
  <section class="bg-gray-100 py-8">
    <div class="container mx-auto px-2 pt-4 pb-12 text-gray-800">
      <h1
        class="w-full my-2 text-5xl font-bold leading-tight text-center text-gray-800"
      >
        Latest Posts
      </h1>
      <div class="w-full mb-4">
        <div
          class="h-1 mx-auto gradient w-64 opacity-25 my-0 py-0 rounded-t"
        ></div>
      </div>

      <div class="container mx-auto flex flex-wrap pt-4 pb-12">
        <div
          class="clickeable w-full md:w-1/3 p-6 flex flex-col flex-grow flex-shrink"
          v-for="post in $static.posts.edges"
          :key="post.node.id"
          v-on:click="goToPost(post.node.url)"
        >
          <div
            class="flex-1 bg-white rounded-t rounded-b-none overflow-hidden shadow"
          >
            <div class="flex flex-wrap no-underline hover:no-underline">
              <div class="w-full font-bold text-xl text-gray-800 px-6 py-6">
                {{ post.node.title | truncate(50, '...') }}
              </div>
              <p class="text-gray-800 text-base px-6 mb-5">
                {{
                  parsedPost(post.node.item.content_encoded)
                    | truncate(250, '...')
                }}
                <!-- <truncate clamp="" :length="255" less="Show Less" type="html" :text="post.node.item.content_encoded"></truncate>  -->
                <br />
                <small>«Read More»</small>
              </p>
            </div>
          </div>
        </div>
      </div>
      <div class="w-full flex justify-center pb-24">
        <a href="https://medium.com/@mmoscosa" target="blank">
          See all my posts
          <g-image class="w-8 h-8 mx-10" src="~/assets/img/medium.png" />
        </a>
      </div>

      <h1
        class="w-full my-2 text-5xl font-bold leading-tight text-center text-gray-800"
      >
        Recommended Books
      </h1>
      <div class="w-full mb-4">
        <div
          class="h-1 mx-auto gradient w-64 opacity-25 my-0 py-0 rounded-t"
        ></div>
      </div>
    </div>

    <div class="container mx-auto flex flex-wrap pt-4 pb-12">
      <table class="table-auto w-full text-gray-900">
        <tbody>
          <tr
            class="clickeable"
            v-for="book in computedBooks"
            :key="book.node.id"
            v-on:click="goToSource(book.node.link)"
          >
            <td class="px-4 py-2">
              <g-image class="rounded w-24" :src="book.node.cover.file.url" />
            </td>
            <td class="px-4 py-2">
              <span class="font-bold">{{ book.node.title }}</span> <br />
              <small>{{ book.node.author }}</small>
            </td>
          </tr>
        </tbody>
      </table>
      <a
        href="#"
        class="w-full my-2 text font-thin leading-tight text-center text-gray-800"
        v-on:click="toggleMore()"
        v-show="$static.books.edges.length > booksLimit"
      >
        Show {{ more === true ? 'less' : 'more' }}
      </a>
    </div>
  </section>
</template>

<static-query>
  query {
  books: allContentfulBooks {
    edges{
      node{
        title,
        author,
        updatedAt,
        cover{
          file{
            url
          }
        },
        link
      }
    }
  },
    posts:
		allBlogPosts(limit: 4, order:ASC){
    edges{
      node{
        id,
        title,
        url,
        created,
        categories,
        item {
          content_encoded
        }
      }
    }
		}

}
</static-query>

<script>
const htmlToText = require('html-to-text')
export default {
  data: function() {
    return {
      more: false,
      booksLimit: 5,
    }
  },
  computed: {
    computedBooks: function() {
      if (this.more) {
        return this.$static.books.edges
      } else {
        return this.$static.books.edges.slice(0, this.booksLimit)
      }
    },
  },
  methods: {
    toggleMore: function() {
      this.more = !this.more
    },
    parsedPost: function(unparsedPost) {
      return htmlToText.fromString(unparsedPost)
    },
    goToSource: function(url) {
      var win = window.open(url, '_blank')
      win.focus()
    },
    goToPost: function(url) {
      var win = window.open(url)
      win.focus()
    },
  },
}
</script>

<style>
.clickeable {
  cursor: pointer;
}
</style>

<template>
  <section class="bg-white border-b py-8">
    <div class="container max-w-5xl mx-auto m-8">
      <h1
        class="w-full my-2 text-5xl font-bold leading-tight text-center text-gray-800"
      >
        About Martin
      </h1>
      <div class="w-full mb-4">
        <div
          class="h-1 mx-auto gradient w-64 opacity-25 my-0 py-0 rounded-t"
        ></div>
      </div>

      <div class="flex flex-wrap">
        <div class="w-5/6 sm:w-1/2 p-3">
          <h3 class="text-3xl text-gray-800 font-bold leading-none mb-3">
            {{ $static.objective.title }}
          </h3>
          <p class="text-gray-600 mb-8" v-html="$static.objective.content"></p>
          <h3 class="text-2xl text-gray-800 font-bold leading-none mb-3">
            Social Media
          </h3>
          <p class="text-gray-600 mb-4">
            You can also follow me on social media to rapidly know what I am up
            to...
          </p>
          <div class="flex flex-row text-gray-800 pb-2">
            <div class="pr-4">
              <a href="https://www.instagram.com/mmoscosa/" target="_blank"
                ><font-awesome :icon="['fab', 'instagram']"
              /></a>
            </div>
            <div class="px-4">
              <a href="https://twitter.com/mmoscosa" target="_blank"
                ><font-awesome :icon="['fab', 'twitter']"
              /></a>
            </div>
            <div class="px-4">
              <a
                href="https://www.youtube.com/channel/UCfZfBpohRrYqLZEHymDNc8g"
                target="_blank"
                ><font-awesome :icon="['fab', 'youtube']"
              /></a>
            </div>
            <div class="px-4">
              <a href="https://www.linkedin.com/in/mmoscosa/" target="_blank"
                ><font-awesome :icon="['fab', 'linkedin']"
              /></a>
            </div>
          </div>
        </div>
        <div class="w-full sm:w-1/2 p-6">
          <div class="embed-responsive aspect-ratio-16">
            <youtube video-id="XixvLyNjw98"></youtube>
          </div>

          <section class="pt-12">
            <lastTweet />
          </section>
        </div>
      </div>

      <div class="flex flex-wrap">
        <div class="w-full p-3">
          <div class="align-middle">
            <h3 class="text-3xl text-gray-800 font-bold leading-none mb-3">
              {{ $static.quickBio.title }}
            </h3>
            <p class="text-gray-600 mb-8" v-html="$static.quickBio.content"></p>
          </div>
        </div>
      </div>
      <div class="flex flex-wrap">
        <div class="w-full p-3">
          <div class="align-middle">
            <h4 class="text-2xl text-gray-800 font-bold leading-none mb-3">
              {{ $static.hobbies.title }}
            </h4>
            <p class="text-gray-600 mb-8" v-html="$static.hobbies.content"></p>
            <youtubeVideos />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<static-query>
query{
	objective:contentfulAbout(id: "6qZ4cAOZWvCH4OcWDE5Vzs"){
    	title,
    	content,
    	side
  },
	quickBio:contentfulAbout(id: "32dcNwLOqp8KmOLfgJCAv"){
    	title,
    	content,
    	side
  },
  hobbies:contentfulAbout(id: "1Nn5SH7tz8wYtr3WQZI9fF"){
    	title,
    	content,
    	side
  }
}
</static-query>
<script>
import youtubeVideos from '~/components/index/Youtube.vue'
import lastTweet from '~/components/index/lastTweet.vue'

export default {
  data: function() {
    return {}
  },
  components: {
    lastTweet,
    youtubeVideos,
  },
}
</script>

<style>
.embed-responsive {
  position: relative;
  display: block;
  height: 0;
  padding: 0;
  overflow: hidden;
}

.embed-responsive .embed-responsive-item,
iframe,
embed,
object,
video {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  height: 100%;
  width: 100%;
  border: 0;
}

.aspect-ratio-square {
  padding-top: 100%;
}

.aspect-ratio-16 {
  padding-top: 56.25%;
}

.aspect-ratio-4 {
  padding-top: 75%;
}

.aspect-ratio-21 {
  padding-top: 42.86%;
}
</style>

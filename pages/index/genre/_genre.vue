<template>
  <div>
    <app-playlist-elem v-for="(playlist, index) in playLists" v-bind:key="index"
                       :playlist="playlist" :currentPlaying="currentPlaylist" :isPlaying="getIsPlaying">
    </app-playlist-elem>
  </div>
</template>

<script>
  import AppPlaylistElem from '~/components/AppPlaylistElem.vue'

  export default {
    components: {
      AppPlaylistElem
    },

    computed: {
      currentPlaylist: function() {
        return this.$store.getters.getCurrentPlaying;
      },
      getIsPlaying: function() {
        return this.$store.getters.getIsPlaying;
      }
    },

    async asyncData({ app, params, error, query }) {
      const { data } = await app.$axios.$get(`https://api.mixcloud.com/discover/${params.genre}/popular/`);
      return { playLists: data }
    }
  }
</script>

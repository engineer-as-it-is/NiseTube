<template>
  <v-container fluid class="d-flex justify-start flex-wrap">
    <nuxt-link v-for="movie in movieList" :key="movie.id" :to="movie.id">
      <v-card class="mx-3 my-5" elevation="0" max-width="400px">
        <v-img
          class="white--text align-end"
          height="200px"
          src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
        ></v-img>    
        <v-list-item>
          <v-list-item-avatar>
            <v-img :src="movie.channel.avatarUrl"></v-img>
          </v-list-item-avatar>            
          <v-list-item-content>
            <v-list-item-title>{{ movie.title }}</v-list-item-title>
            <v-list-item-subtitle>{{ movie.channel.name }}</v-list-item-subtitle>
            <v-list-item-subtitle>{{ movie.views }}回視聴・{{ movie.postedAt }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-card>
    </nuxt-link>
  </v-container>
</template>

<script>
  export default {
    props: {
      source: String,
    },
    data: () => ({
      drawer: null,
      items: [
        { icon: 'trending_up', text: 'Most Popular' },
        { icon: 'subscriptions', text: 'Subscriptions' },
        { icon: 'history', text: 'History' },
        { icon: 'featured_play_list', text: 'Playlists' },
        { icon: 'watch_later', text: 'Watch Later' },
      ],
      items2: [
        { picture: 28, text: 'Joseph' },
        { picture: 38, text: 'Apple' },
        { picture: 48, text: 'Xbox Ahoy' },
        { picture: 58, text: 'Nokia' },
        { picture: 78, text: 'MKBHD' },
      ],
      movieList: []
    }),
    created () {
      this.$vuetify.theme.dark = true
      for(let i=0; i<10; i++) {
        this.movieList.push(        {
          id: `movie${i}`,
          title: `サンプル動画${i}`,
          channel: {
            name: `エンジニアのリアルチャンネル${i}`,
            avatarUrl: `https://randomuser.me/api/portraits/men/${i}.jpg`
          },
          views: Math.floor(Math.random() * 100000),
          postedAt: `${i}日前`
        })
      }
    },
  }
</script>

<style scoped>
a {
  text-decoration: none;
}
</style>
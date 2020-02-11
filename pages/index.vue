<template>
  <v-container fluid class="d-flex justify-start flex-wrap">
    <nuxt-link v-for="movie in movieList" :key="movie.id" :to="movie.id">
      <v-card class="mx-3 my-5" elevation="0" max-width="400px">
        <v-img
          class="white--text align-end"
          height="200px"
          :src= movie.thumbnailUrl
        ></v-img>    
        <v-list-item>
          <v-list-item-avatar>
            <v-img :src="movie.avatarUrl"></v-img>
          </v-list-item-avatar>            
          <v-list-item-content>
            <v-list-item-title>{{ movie.title }}</v-list-item-title>
            <v-list-item-subtitle>{{ movie.channelName }}</v-list-item-subtitle>
            <v-list-item-subtitle>{{ movie.views }}回視聴・{{ movie.postedAt }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-card>
    </nuxt-link>
  </v-container>
</template>

<script>
import { API, graphqlOperation } from 'aws-amplify';
import * as queries from '~/src/graphql/queries';

  export default {
    props: {
      source: String,
    },
    data: () => ({
      drawer: null,
      movieList: []
    }),
    async created () {
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
      const result = await this.getAllPosts()
      this.movieList = result.data.listPosts.items
    },
    methods: {
      async getAllPosts() {
        return await API.graphql(graphqlOperation(queries.listPosts));
      }
      // Simple query

    }
  }
</script>

<style scoped>
a {
  text-decoration: none;
}
</style>

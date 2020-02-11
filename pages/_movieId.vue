<template>
    <v-container>
        <hls v-if="movie.movieUrl" class="movie" :movieUrl="movie.movieUrl"></hls>
        <v-list-item>
            <v-list-item-content>
                <v-list-item-title>{{ movie.title }}</v-list-item-title>
                <v-list-item-subtitle>{{ movie.views }}回視聴・{{ movie.postedAt }}</v-list-item-subtitle>
            </v-list-item-content>
        </v-list-item>
        <v-divider />           
        <v-list-item>
            <v-list-item-avatar>
                <v-img :src="movie.avatarUrl"></v-img>
            </v-list-item-avatar>
            <v-list-item-content>
                <v-list-item-title>{{ movie.channeName }}</v-list-item-title>
                <v-list-item-subtitle>チャンネル登録者数　1億人</v-list-item-subtitle>
            </v-list-item-content>
            <v-list-item-action>
                <v-btn color="red" @click="() => alert('チャンネル登録機能はメンテナンス中tyuu')">チャンネル登録</v-btn>
            </v-list-item-action>
        </v-list-item>
    </v-container>
</template>

<script>
import { API, graphqlOperation } from 'aws-amplify';
import * as queries from '~/src/graphql/queries';

import hls from '@/components/hls'

export default {
    components: {
        hls
    },
    data() {
        return {
            movie: {}
        }
    },
    async created () {
      const result = await this.getPostByID(this.$route.params.movieId)
      this.movie = result.data.getPost
    },
    methods: {
      async getPostByID(id) {
        return await API.graphql(graphqlOperation(queries.getPost, { id: id }));
      }
    }
}
</script>

<style scoped>
.movie {
    width: 100%;
}
</style>

<template>
    <v-container>
        <!-- <hls class="movie" movieUrl="http://nisetube-download-work.s3-website-ap-northeast-1.amazonaws.com/sample-movie1/sample-movie1.m3u8"></hls> -->
        <hls v-if="movie.movieUrl" class="movie" :movieUrl="movie.movieUrl"></hls>
        <!-- <hls class="movie" :movieUrl="movie.movieUrl"></hls> -->
        <!-- {{ movie.movieUrl }} -->
        <v-list-item>
            <v-list-item-content>
                <v-list-item-title>{{ movie.title }}</v-list-item-title>
                <v-list-item-subtitle>{{ movie.views }}回視聴・{{ movie.postedAt }}</v-list-item-subtitle>
                <!-- <v-list-item-action>
                    <v-btn icon>
                        <v-icon left>mdi-thumbs-up-outline</v-icon>
                        {{ movie.review.good }}
                    </v-btn>
                    <v-btn icon>
                        <v-icon left>mdi-thumbs-down-outline</v-icon>
                        {{ movie.review.bad }}
                    </v-btn>
                </v-list-item-action> -->
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
                <v-btn color="red" >チャンネル登録</v-btn>
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
            // movie: {
            //     title: 'サンプル動画',
            //     description: '今日はとんかつ屋さんへ行ってきました♪',
            //     views: 300,
            //     postedAt: '2020/01/01',
            //     channel: {
            //         name: 'サンプルチャンネル',
            //         avatarUrl: `https://randomuser.me/api/portraits/men/1.jpg`,
            //         subscribers: 10
            //     },
            //     review: {
            //         good: 2,
            //         bad: 1
            //     }
            // }
            movie: {}
        }
    },
    async created () {
    //   this.$vuetify.theme.dark = true
    //   for(let i=0; i<10; i++) {
    //     this.movieList.push(        {
    //       id: `movie${i}`,
    //       title: `サンプル動画${i}`,
    //       channel: {
    //         name: `エンジニアのリアルチャンネル${i}`,
    //         avatarUrl: `https://randomuser.me/api/portraits/men/${i}.jpg`
    //       },
    //       views: Math.floor(Math.random() * 100000),
    //       postedAt: `${i}日前`
    //     })
    //   }
        console.log(this.$route.params.movieId)
      const result = await this.getPostByID(this.$route.params.movieId)
      console.log(result)
      this.movie = result.data.getPost
    //   this.movieList = result.data.listPosts.items
    },
    methods: {
      async getPostByID(id) {
        return await API.graphql(graphqlOperation(queries.getPost, { id: id }));
      }
      // Simple query

    }
}
</script>

<style scoped>
.movie {
    width: 100%;
}
</style>

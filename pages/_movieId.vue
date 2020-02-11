<template>
    <v-container>
        <hls class="movie" movieUrl="http://nisetube-download-work.s3-website-ap-northeast-1.amazonaws.com/sample-movie1/sample-movie1.m3u8"></hls>
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
                <v-img :src="movie.channel.avatarUrl"></v-img>
            </v-list-item-avatar>
            <v-list-item-content>
                <v-list-item-title>{{ movie.channel.name }}</v-list-item-title>
                <v-list-item-subtitle>チャンネル登録者数　{{ movie.channel.subscribers }}人</v-list-item-subtitle>
            </v-list-item-content>
            <v-list-item-action>
                <v-btn color="red" >チャンネル登録</v-btn>
            </v-list-item-action>
        </v-list-item>
    </v-container>
</template>

<script>
import hls from '@/components/hls'

export default {
    components: {
        hls
    },
    created() {
        console.log(this.$route)
    },
    data() {
        return {
            movie: {
                title: 'サンプル動画',
                description: '今日はとんかつ屋さんへ行ってきました♪',
                views: 300,
                postedAt: '2020/01/01',
                channel: {
                    name: 'サンプルチャンネル',
                    avatarUrl: `https://randomuser.me/api/portraits/men/1.jpg`,
                    subscribers: 10
                },
                review: {
                    good: 2,
                    bad: 1
                }
            }
        }
    }
}
</script>

<style scoped>
.movie {
    width: 100%;
}
</style>

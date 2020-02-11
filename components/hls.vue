<template>
	<video ref="video" controls></video>
</template>

<script>
import Hls from 'hls.js'

export default {
    props: [
        'movieUrl'
    ],
    mounted () {
        if (Hls.isSupported()) {
            const hls = new Hls()
            hls.loadSource(this.movieUrl)

            const video = this.$refs.video
            hls.attachMedia(video)
        }
    }
}

</script>

<style lang="scss">
</style>
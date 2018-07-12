<template>
  <div>
    <audio id="talAudio"
           controls="controls"
           preload
           :class="{hide: !show, show: show}"
           ref="talAudio"
           @timeupdate="playerCurTimeUpdated"
           :src="src"></audio>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    data() {
      return {
        playProcess: 0,
        canPlay: false,
        audioLeft: 0,
        isPaused: true
      }
    },
    props: {
      src: {
        type: String,
        default: ''
      },
      show: {
        type: Boolean,
        default: true
      }
    },
    methods: {
      playerCurTimeUpdated() {
        let audio = this.$refs['talAudio']
        let cur = Math.floor(audio.currentTime)
        if (cur > this.playProcess) {
          this.playProcess = cur
          this.$emit('currentTimeUpdated', this.playProcess)
        }
      }
    },
    computed: {},
    mounted() {
      let audio = this.$refs['talAudio']
      // play
      this.$on('play', (time) => {
        if (!this.canPlay) return false
        if (time) {
          audio.currentTime = time
          audio.play()
        } else {
          console.log('play')
          audio.play()
          this.isPaused = false
          this.$emit('playStateChanged', {isPaused: this.isPaused})
        }
      })
      // pause
      this.$on('pause', () => {
        console.log('paused')
        audio.pause()
        this.isPaused = true
        this.$emit('playStateChanged', {isPaused: this.isPaused})
      })
      // stop
      this.$on('stop', () => {
        console.log('stop')
        audio.currentTime = this.duration
        this.audioLeft = this.duration
        this.isPaused = true
        this.$emit('playStateChanged', {isPaused: this.isPaused})
      })

      // listening canplay and ended event
      let dom = document.getElementById('talAudio')
      this.$nextTick(() => {
        dom.addEventListener('canplay', () => {
          console.log('canplay')
          this.duration = Math.floor(dom.duration)
          this.audioLeft = this.duration
          this.canPlay = true
          this.$emit('readyToPlay', {canPlay: this.canPlay, duration: dom.duration})
        })
        dom.onended = () => {
          console.log('ended')
          this.audioLeft = Math.floor(dom.duration)
          this.isPaused = true
          this.playProcess = 0
          this.$emit('playStateChanged', {isPaused: this.isPaused})
        }
      })
    }
  }
</script>

<style>
  .hide {
    display: none;
  }
  .show {
    display: block;
  }
</style>

<template>
    <div class="audition-report">
        <div>
            <button @click="testPlay">播放</button>
            <button @click="testPause">暂停</button>
            <button @click="testStop">停止</button>
            <p>总时间：{{testDuration}}，当前时间：{{testCurrent}}</p>
            <talAudio :src="'http://s1.test-www.qdsay.com/static/audio/loveIsLongerThanLetters.mp3'"
                      :show="true"
                      ref="aTandT"
                      @readyToPlay="getReady"
                      @playStateChanged="playStateChanged"
                      @currentTimeUpdated="curUped"
            ></talAudio>
        </div>
    </div>
    </div>
</template>

<script type="text/ecmascript-6">
    import talAudio from '~/components/layOut/talAudio'
    export default {

        data () {
            return {
                testDuration: 0,
                testCurrent: 0
            }
        },
        components: {
            talAudio
        },
        methods: {
            playStateChanged(d) {
                console.log(d)
            },
            testPlay() {
                this.$refs['aTandT'].$emit('play', 100)
            },
            testPause() {
                this.$refs['aTandT'].$emit('pause')
            },
            testStop() {
                this.$refs['aTandT'].$emit('stop')
            },
            getReady(d) {
                this.testDuration = d.duration
            },
            curUped(d) {
                this.testCurrent = d
            }
        }
    }
</script>


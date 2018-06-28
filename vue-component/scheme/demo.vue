<template>
  <div>
    <el-button @click="reset">重置</el-button>
    <el-button @click="thisWeek">本周</el-button>
    <el-button @click="nextWeek">下周</el-button>
    <scheme :now="now"
            @receiveScheme="handleScheme"
            ref="schemeRef" ></scheme>
  </div>
</template>

<script type="text/ecmascript-6">
  import scheme from '~/components/layout/scheme'
  export default {
    data() {
      return {
        now: new Date()
      }
    },
    methods: {
      handleScheme(d) {
        console.log(d)
      },
      reset() {
        this.$refs['schemeRef'].$emit('resetScheme', true)
      },
      nextWeek() {
        if (this.now.getDate() === (new Date().getDate() + 7)) return false
        this.now = new Date(new Date().getTime() + 7 * 24 * 60 * 60 * 1000)
      },
      thisWeek() {
        this.now = new Date()
      }
    },
    components: {
      scheme
    },
    mounted() {}
  }
</script>

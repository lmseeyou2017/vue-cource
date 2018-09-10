<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/img/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <b>{{ food }}</b>
    <button @click="handleClick('back')">返回上一页</button>
    <button @click="handleClick('push')">跳转到parent</button>
    <button @click="handleClick('replace')">跳转到parent</button>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    HelloWorld
  },
  props: {
    food: {
      type: String,
      default: 'apple'
    }
  },
  beforeRouteEnter (to, from, next) {
    // this 不可用
    // console.log('to: ' + to.name)
    // console.log('from: ' + from.name)
    next(vm => {
      console.log(vm)
    })
  },
  beforeRouteLeave (to, from, next) {
    const leave = confirm('您确定要离开吗？')
    if (leave) next()
    else next(false)
  },
  methods: {
    handleClick (type) {
      if (type === 'back') this.$router.go(-1)
      else if (type === 'push') {
        const name = 'lison'
        this.$router.push({
          path: `/argu/${name}`

        })
      } else if (type === 'replace') {
        this.$router.replace({
          name: 'parent'
        })
      }
    }
  }
}
</script>

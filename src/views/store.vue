<template>
  <div>
    <a-input @input="inputHandle" />
    <p>{{ inputValue }} -> lasterLetter is {{ inputValueLasterLetter }}</p>
    <a-show :content="inputValue" />
    <p>appName: {{appName}} , appNameWithVersion : {{ appNameWithVersion }}</p>
    <p> userName : {{ userName }} , firstLetter: {{ firstLetter }}</p>
  </div>
</template>

<script>
import AInput from '_c/AInput.vue'
import AShow from '_c/AShow.vue'
import { mapState, mapGetters } from 'vuex'
// const {  } = createNamespacedHelpers('user')
export default {
  name: 'store',
  data () {
    return {
      inputValue: ''
    }
  },
  components: {
    AInput,
    AShow
  },
  computed: {
    ...mapState({
      appName: state => state.appName,
      userName: state => state.user.userName
    }),
    ...mapGetters([
      'firstLetter'
    ]),
    inputValueLasterLetter () {
      return this.inputValue.substr(-1, 1)
    },
    /*     appName () {
      return this.$store.state.appName
    },
    userName () {
      return this.$store.state.user.userName
    } */
    appNameWithVersion () {
      return this.$store.getters.appNameWithVersion
    }
  },
  methods: {
    inputHandle (val) {
      this.inputValue = val
    }
  }
}
</script>

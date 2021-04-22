<template>
  <section class="KForm">
    <slot></slot>
  </section>
</template>

<script>
export default {
  name: 'KForm',
  provide () {
    return {
      form: this
    }
  },
  props: {
    model: {
      type: Object,
      required: true
    },
    rules: {
      type: Object
    }
  },
  data () {
    return {}
  },
  components: {},
  watch: {},
  mounted () {},
  methods: {
    validate (cb) {
      //  获取所有的Items并执行他们的validate
      const tasks = this.$children
        .filter(item => item.prop)
        .map(item => item.validate())
        console.log("tasks",tasks)
      // 判断结果
      Promise.all(tasks)
        .then(() => {
          cb(true)
          console.log("true")
        })
        .catch(() => {
            cb(false)
        })
    }
  }
}
</script>

<style scoped lang="less"></style>

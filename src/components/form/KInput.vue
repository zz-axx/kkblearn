<template>
  <section class="kinput">
    <!-- v-model实现：value + $emit（'input',e.target.value） -->
    <!-- v-bind="$attrs"   自动展开 -->
    <input :type="type" :value="value" @input="onInput" v-bind="$attrs" />
  </section>
</template>

<script>
export default {
  name: 'kinput',
  inheritAttrs: false, // 关掉$attrs的继承属性
  props: {
    type: {
      type: String,
      default: 'text'
    },
    value: {
      type: String,
      required: true
    }
  },
  data () {
    return {}
  },
  components: {},
  watch: {},
  mounted () {},
  methods: {
    onInput (e) {
      this.$emit('input', e.target.value)
      //  让老爹去派发事件
      this.$parent.$emit('validate')
    }
  }
}
</script>

<style scoped lang="less"></style>

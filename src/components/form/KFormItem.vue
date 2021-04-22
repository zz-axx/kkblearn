<template>
  <section class="KFormItem">
    <!-- label -->
    <label v-if="label">{{ label }}</label>
    <!-- 插槽 -->
    <slot></slot>
    <!-- 错误提示 -->
    <p v-if="error">{{ error }}</p>
    <!-- inject -->
    <!-- <p>{{ form.rules[prop] }}</p> -->
  </section>
</template>

<script>
import Schema from 'async-validator'
export default {
  name: 'KFormItem',
  inject: ['form'],
  props: {
    label: {
      type: String,
      default: ''
    },
    prop: {
      type: String
    }
  },
  data () {
    return {
      error: ''
    }
  },
  components: {},
  watch: {},
  mounted () {
    this.$on('validate', () => {
      this.validate()
    })
  },
  methods: {
    validate () {
      //  拿到校验值和校验规则
      const value = this.form.model[this.prop]
      const rules = this.form.rules[this.prop]
          console.log("values",value)

      
        // 创建校验器
        const validator = new Schema({ [this.prop]: rules })
        return validator.validate({ [this.prop]: value }, errors => {
          if (errors) {
            console.log(errors)
            this.error = errors[0].message
          } else {
            this.error = ''
          }
        })
      
    }
  }
}
</script>

<style scoped lang="less"></style>

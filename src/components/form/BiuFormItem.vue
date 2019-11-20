<template>
    <div>
        <p v-show="label">{{label}}</p>
        <slot></slot>
        <p class="error" v-show="error">{{error}}</p>
    </div>
</template>

<script>
import Schema from 'async-validator'

export default {
    inject: ['BiuForm'],
    props: {
        label: [Number, String],
        prop: String
    },
    data () {
        return {
            error: ''
        }
    },
    mounted () {
        this.$on('validate', () => {
            this.validate()
        })
    },
    methods: {
        validate () {
            // 获取值和规则
            let value = this.BiuForm.model[this.prop]
            let rule = this.BiuForm.rules[this.prop]
            let schema = new Schema({[this.prop]: rule})
            return schema.validate({[this.prop]: value}, errors => { // 返回一个promise给form
                if (errors) {
                    this.error = errors[0].message
                } else {
                    this.error = ''
                }
            })
        }
    }
}
</script>

<style>
.error {
    color: red;
}
</style>
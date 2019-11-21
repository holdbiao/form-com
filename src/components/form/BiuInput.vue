<template>
    <div>
        <input :value="value" @input="onInput" v-bind="$attrs" :class="[{'input-error': isError}]">
    </div>
</template>

<script>
export default {
    inheritAttrs: false, // $attrs默认行为将会被去掉
    props: {
        value: [Number, String]
    },
    data () {
        return {
            isError: false
        }
    },
    methods: {
        onInput (e) {
            this.$emit('input', e.target.value)
            this.$emit('update:value', e.target.value)
            this.$parent.$emit('validate') // 让父级派发事件
        }
    },
    computed: {
        parentError () {
            return this.$parent.error
        }
    },
    watch: {
        parentError (ne) { // 借助computed监听父级对象
            this.isError = !!ne
        }
    }
}
</script>

<style>
input {
    outline: none;
}
.input-error {
    border: 1px solid red;
}
</style>
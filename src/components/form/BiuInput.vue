<template>
    <div>
        <input :value="value" @input="onInput" v-bind="$attrs">
    </div>
</template>

<script>
export default {
    inheritAttrs: false, // $attrs默认行为将会被去掉
    props: {
        value: [Number, String]
    },
    methods: {
        onInput (e) {
            this.$emit('input', e.target.value)
            this.$emit('update:value', e.target.value)
            this.$parent.$emit('validate') // 让父级派发事件
        }
    }
}
</script>

<style>

</style>
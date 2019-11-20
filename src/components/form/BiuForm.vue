<template>
    <div>
        <slot></slot>
    </div>
</template>

<script>
export default {
    provide () {
        return {
            'BiuForm': this
        }
    },
    props: {
        model: {
            type: Object,
            required: true,
            default: () => {}
        },
        rules: {
            type: Object
        }
    },
    methods: {
        validate (callback) {
            // console.log('全局校验')
            const tasks = this.$children
                .filter(child => child.prop) // 只留下有prop的child
                .map(child => child.validate()) // 返回promise数组
            // promise数组全部then才会走到then
            console.log(tasks)
            Promise.all(tasks)
                .then(() => callback(true))
                .catch(() => callback(false))
        }
    }
}
</script>

<style>

</style>
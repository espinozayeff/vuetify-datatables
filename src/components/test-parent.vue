<template>
    <section>
        <slot v-for="(_, name) in $slots" :name="name" :slot="name" />
        <template v-for="(_, name) in $scopedSlots">
            <slot :name="name" />
        </template>
    </section>
</template>

<script>
export default {
    name: 'test-parent',
    props: ['child'],
    mounted() {
        console.log('$slots', this.$slots)
        console.log('$scopedSlots', this.$scopedSlots)
    },
}
</script>

<style scoped></style>

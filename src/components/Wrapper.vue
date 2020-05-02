<template>
    <component :is="child">
        <slot v-for="(_, name) in $slots" :name="name" :slot="name" />
        <template
            v-for="(_, name) in $scopedSlots"
            :slot="name"
            slot-scope="slotData"
        >
            <slot :name="name" v-bind="slotData" />
        </template>
    </component>
</template>

<script>
export default {
    name: 'Wrapper',
    props: ['child'],
}
</script>

<style scoped></style>

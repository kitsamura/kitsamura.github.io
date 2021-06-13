<template>
    <div>
        <div class="table__main_el">
            <div class="table__el_name">
                {{name}}
            </div>
            <div class="table__el_phone">
                {{phone}}
            </div>
        </div>
        <template v-if="children">
                <div class="uuu">
                <Element v-for="child in children" :key="child.id" :name="child.name" :phone="child.phone"
                :chief="child.chief" :children="child.children" />
                </div>
        </template>
    </div>
</template>

<script>
    export default {
        name: 'Element',
        props: ['name', 'phone', 'children'],
        methods: {

        },
    }
</script>

<style scoped>
    .uuu{
        padding-left: 10px;
    }
</style>
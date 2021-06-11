<template>
    <div class="table__main_el">
        <div class="table__el_name">
            {{name}}
        </div>
        <div class="table__el_phone">
            {{phone}}
        </div>
    </div>
</template>

<script>
export default {
    props: ['name', 'phone'],
}
</script>
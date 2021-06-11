<template>
  <div>
    <Multiselect v-model="value" placeholder="Выберете начальника" :options="elems" @input="clickOption" />
  </div>
</template>

<script>
  import Multiselect from '@vueform/multiselect'

  export default {
    components: {
      Multiselect
    },
    data() {
      return {
        value: null,
        elems: [
          'Алексей', 'Михаил', 'Евгения'
        ],
      }
    },
    methods: {
      clickOption(value) {
        this.$emit('addChief', value)
      }
    }
  }
</script>

<style src="@vueform/multiselect/themes/default.css"></style>
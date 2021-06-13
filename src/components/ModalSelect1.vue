<template>
  <div>
    <Multiselect v-model="value" placeholder="Выберете начальника" :options="elems"
      @input="clickOption" @click="clicker"/>
  </div>
</template>

<script>
  import Multiselect from '@vueform/multiselect'

  export default {
    props: ['elems'],
    components: {
      Multiselect
    },
    data() {
      return {
        type: Array,
        value: null,
      }
    },
    methods: {
      clickOption(value) {
        // console.log(value);
        this.$emit('addChief', value)
      },
      clicker(){
        console.log(this.options);
      }
    }
  }
</script>

<style src="@vueform/multiselect/themes/default.css"></style>
<template>
  <div class="modal__select">
    <p class="modal__select_title" @click="areOptionsVisible = !areOptionsVisible">{{selected}}</p>
      <div class="modal__select_options"
      v-if="areOptionsVisible">
      <p class="modal__select_option" v-for="option in options" :key="option.id" @click="selectOption(option)">
        {{option.name}}
      </p>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      options: {
        type: Array,
        default () {
          return []
        }
      },
      selected: {
        type: String,
        default: ''
      }
    },
    data() {
      return {
        areOptionsVisible: false, 
      }
    },
    methods: {
      clickOption(value) {
        // console.log(value);
        this.$emit('addChief', value)
      },
      selectOption(option) {
        console.log(option.id);
        this.$emit('selectedOption', option)
        this.areOptionsVisible = false;
      }
    }
  }
</script>

<style>
  .modal__select {
    cursor: pointer;
    position: relative;
    margin: 0 auto;
  }

  .modal__select_options {
    position: absolute;
    top: 20px;
    width: 100%;
    /* left: 0;
    right: 0; */
    border: 1px solid #aeaeae;
    /* margin-top: -1px; */
    max-height: 160px;
    overflow-y: scroll;
    -webkit-overflow-scrolling: touch;
    z-index: 100;
    background: #fff;
    display: flex;
    flex-direction: column
  }

  .modal__select_title {
        border: 1px solid #aeaeae;
  }

  /* .open-top .multiselect-options {

    transform: translateY(-100%);
    top: 2px;
    flex-direction: column-reverse
  } */

  .modal__select_option {
    display: flex;
    min-height: 10px;
    padding: 9px 12px;
    box-sizing: border-box;
    color: #000000;
    /* text-decoration: none; */
    align-items: center;
    justify-content: flex-start;
    text-align: left;
    cursor: pointer;
  }

  /* .multiselect-option.is-pointed {
    background: #e6e6e6
  } */
  .modal__select_option:hover {
    background: #ededff;
    color: #ffffff;
  }

  @-webkit-keyframes spinning {
    0% {
      transform: rotate(0)
    }

    to {
      transform: rotate(2turn)
    }
  }

  @keyframes spinning {
    0% {
      transform: rotate(0)
    }

    to {
      transform: rotate(2turn)
    }
  }
</style>
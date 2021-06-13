<template>
  <div class="modal__select">
    <p class="modal__select_title" @click="areOptionsVisible = !areOptionsVisible">{{selected}} <i
        class="material-icons modal__select_icon">expand_more</i></p>
    <div class="modal__select_options" v-if="areOptionsVisible">
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
    top: 41px;
    width: 100%;
    border: 1px solid #f4f4f4;
    max-height: 124px;
    overflow-y: scroll;
    -webkit-overflow-scrolling: touch;
    z-index: 100;
    background: #fff;
    display: flex;
    flex-direction: column
  }

  .modal__select_title {
    position: relative;
    border: 1px solid #f4f4f4;
    border-radius: 4px;
    box-sizing: border-box;
    margin: 0px;
    height: 42px;
    padding: 8px 0px 0px 15px;
    margin-top: 2px;
    text-align: left;
    width: 100%;
    font-size: 20px;
    line-height: 25px;
    color: var(--text-color);
    font-weight: var(--text-light);
    font-family: var(--font);
  }

  .modal__select_icon {
    position: absolute;
    right: 7px;
    top: 8px;
  }

  .open-top {
    transform: translateY(-100%);
    top: 2px;
    flex-direction: column-reverse
  }

  .modal__select_option {
    display: flex;
    min-height: 40px;
    margin: 0px;
    padding: 9px 12px;
    box-sizing: border-box;
    color: var(--text-color);
    font-weight: 300;
    align-items: center;
    justify-content: flex-start;
    text-align: left;
    cursor: pointer;
  }
  .modal__select_option:hover {
    background: #ededff;
    color:var(--text-color);
  }
</style>
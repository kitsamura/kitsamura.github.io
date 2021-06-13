<template>
    <div class="form__add">
        <form @submit.prevent="onSubmit">
            <div class="form__add_main">
                <span class="form__add_title">Добавление сотрудника</span>
                <Close @click="closeModal" />
                <div class="form__item_wrapper">
                    <label class="form__item_lbl" for="">Начальник</label>
                    <div class="form__item form__select_wrapper">
                        <ModalSelect :options="elems" :selected="selected " @selectedOption="selectedOption" @addChief="addChief" v-model="chief"/>
                    </div>
                </div>
                <div class="form__item_wrapper">
                    <div class="form__item" @keypress="btnChange">
                        <label class="form__item_lbl">Имя</label>
                        <input class="form__item_text" type="text" v-model="name" placeholder="Введите имя" minlength=2>
                    </div>
                </div>
                <div class="form__item_wrapper">
                    <div class="form__item">
                        <label class="form__item_lbl" for="">Телефон</label>
                        <input class="form__item_phone" v-model="phone" @keypress="isNumber($event)"
                            placeholder="Введите телефон" type="phone" maxlength=11 minlength=11 @keyup="btnChange">
                    </div>
                </div>
            </div>
            <div class="form__add_btn_flex">
                <button :disabled=" isDisabled" :class="{disabled: isDisabled}" type="submit" class="form__add_btn">
                    Сохранить
                </button>
            </div>
        </form>
    </div>
</template>

<script>
    import Close from './Close'
    import ModalSelect from './ModalSelect'

    export default {
        props: ['elems'],
        data() {
            return {
                chief: '',
                name: '',
                phone: '',
                selected: 'Выберите начальника', 
            }
        },
        computed: {
            isDisabled: function () {
                return !(this.name && this.phone);
            }},
            components: {
                ModalSelect,
                Close,
            },
            methods: {
                closeModal() {
                    this.$emit('closeModal')
                },
                onSubmit() {
                    this.$emit('onSubmit')
                    this.$emit('closeModal')
                    if (this.name.trim() && this.phone.trim() && (this.name.length > 0) && (this.phone.length > 0)) {

                        const newElem = {
                            id: Date.now(),
                            name: this.name,
                            phone: this.phone,
                            chief: this.chief
                        }
                        this.$emit('addElem', newElem)
                    }
                },
                isNumber(evt) {
                    evt = (evt) ? evt : window.event;
                    var charCode = (evt.which) ? evt.which : evt.keyCode;
                    if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
                        evt.preventDefault();
                    } else {
                        return true;
                    }
                },
                addChief(value) {
                    this.chief = value;
                },
                selectedOption(option) {
                    this.selected=option.name;
                    console.log(this.selected);
                }
            }
        }
</script>

<style>
    .form__add {
        position: fixed;
        box-shadow: 0 5px 24px 0 rgba(0, 0, 0, 0.12);
        padding: 44px 64px 56px 64px;
        background: #ffffff;
        top: 104px;
        right: 0;
        bottom: 0;
        left: 0;
        z-index: 200;
        max-width: 442px;
        margin: 56px auto;
        max-height: 428px;
        animation-duration: 1.5s;
        animation-name: fadein;
        overflow-y: scroll;
        border-radius: 6px;
    }

    .form__add_title {
        display: inline-block;
        font-weight: var(--text-weight);
        color: var(--text-color);
        font-size: 24px;
        line-height: 48px;
        text-align: center;
        margin-bottom: 32px;
        position: relative;
    }

    .form__add_close {
        cursor: pointer;
        position: absolute;
        right: 33px;
        top: 24px;
    }

    .form__item {
        width: 440px !important;
        height: 40px;
        margin-bottom: 44px;
    }

    .form__item_lbl {
        text-align: start;
        display: block;
        font-size: 14px;
        line-height: 24px;
        padding-left: 16px;
        color: var(--text-color);
    }

    .form__item_text,
    .form__item_phone {
        width: 440px !important;
        padding-left: 16px;
        padding-bottom: 8px;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #F4F4F4;
        font-size: 20px;
        line-height: 24px;
        color: var(--text-color);
        font-weight: var(--text-light);
        font-family: var(--font);
    }

    .form__item_phone::placeholder,
    .form__item_text::placeholder {
        font-family: var(--font);
        font-weight: var(--text-light);
    }

    .disabled {
        opacity: 0.5;
    }

    .form__item_phone:focus,
    .form__item_text:focus {
        outline: none;
        border-bottom: 1px solid #9f6ad4;
    }
</style>
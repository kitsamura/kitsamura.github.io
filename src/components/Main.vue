<template>
    <div>
        <Header />
        <main>
            <div class="container">
                <div class="table__flex">
                    <div class="table__main">
                        <div class="table__el_title table__main_el">
                            <div class="table__el_name table__el_name_sort bold" @click="sortElem">
                                Имя
                                <i class="material-icons icon_sort" v-if="sortedName">expand_more</i>
                                <i class="material-icons icon_sort" v-if="unsortedName">expand_less</i>
                            </div>
                            <div class="table__el_phone bold table__el_name_sort bold" @click="sortPhone">
                                Телефон
                                <i class="material-icons icon_sort" v-if="sortedPhone">expand_more</i>
                                <i class="material-icons icon_sort" v-if="unsortedPhone">expand_less</i>
                            </div>
                        </div>
                        <Element v-for="(elem) in elems" :key="elem.id" :name="elem.name" :phone="elem.phone"
                            :chief="elem.chief" :children="elem.children" />
                    </div>
                    <Btn @click="openModal" />
                </div>
            </div>
        </main>
        <Modal :elems="elems" :children="children" v-if="modalIsOpen" @closeModal="closeModal" @click="modalChildren"
            @addElem="addElem" />
    </div>
</template>

<script>
    import Header from './Header'
    import Btn from './Btn'
    import Modal from './Modal'
    import Element from './Element'

    export default {
        data() {
            return {
                modalIsOpen: false,
                sortedName: true,
                unsortedName: false,
                sortedPhone: true,
                unsortedPhone: false,
                children: [],
                elems: [{
                        id: 1,
                        name: 'Алексей',
                        phone: '89063457854',
                        chief: '',
                        children: [{
                            id: 10,
                            name: '• Камиль',
                            phone: '89999990002',
                            chief: 'Алексей',
                            children: [],
                        }],
                    },
                    {
                        id: 2,
                        name: 'Михаил',
                        phone: '89995646767',
                        chief: '',
                        children: [],
                    },
                    {
                        id: 3,
                        name: 'Евгения',
                        phone: '89266459890',
                        chief: '',
                        children: [],
                    },
                ]
            }
        },
        components: {
            Header,
            Btn,
            Modal,
            Element,
        },
        methods: {
            modalChildren() {
                this.children = [];
                this.elems.forEach(elem => {
                    if (elem.children.length > 0) {
                        for (let i = 0; i < elem.children.length; i++) {
                            this.children.push(elem.children[i]);
                        }
                    }
                });
            },
            openModal() {
                this.modalIsOpen = true;
            },
            closeModal() {
                this.modalIsOpen = false;
            },
            addElem(elem) {
                if (elem.chief) {

                    for (let i = 0; i < this.elems.length; i++) {


                        if (elem.chief == this.elems[i].id) {

                            this.elems[i].children.push(elem);
                        }
                    }
                    for (let i = 0; i < this.children.length; i++) {


                        if (elem.chief == this.children[i].id) {

                            this.children[i].children.push(elem);
                        }
                    }
                    this.saveElems();
                } else {

                    this.elems.push(elem);
                    this.saveElems();
                }
            },
            saveElems() {
                let parsed = JSON.stringify(this.elems);
                localStorage.setItem('elems', parsed);
            },
            sortElem() {
                function compareReverse(b, a) {
                    if (a.name < b.name)
                        return -1;
                    if (a.name > b.name)
                        return 1;
                    return 0;
                }

                function compare(a, b) {
                    if (a.name < b.name)
                        return -1;
                    if (a.name > b.name)
                        return 1;
                    return 0;
                }
                if (this.sortedName) {
                    this.sortedName = false;
                    this.unsortedName = true;
                    this.elems.sort(compare)
                } else {
                    this.sortedName = true;
                    this.unsortedName = false;
                    this.elems.sort(compareReverse);
                }
            },
            sortPhone() {
                function compareReverse(b, a) {
                    if (a.phone < b.phone)
                        return -1;
                    if (a.phone > b.phone)
                        return 1;
                    return 0;
                }

                function compare(a, b) {
                    if (a.phone < b.phone)
                        return -1;
                    if (a.phone > b.phone)
                        return 1;
                    return 0;
                }
                if (this.sortedPhone) {
                    this.sortedPhone = false;
                    this.unsortedPhone = true;
                    this.elems.sort(compareReverse)
                } else {
                    this.sortedPhone = true;
                    this.unsortedPhone = false;
                    this.elems.sort(compare);
                }
            }
        },
        mounted() {
            if (localStorage.getItem('elems')) {
                this.elems = JSON.parse(localStorage.getItem('elems'));
            }
        },
    }
</script>

<style>
    main {
        padding-top: 96px;
    }

    .table__flex {
        display: flex;
        justify-content: center;
        flex-direction: column;
        align-items: center;
    }

    .table__main {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        box-shadow: 0 0 31px rgba(0, 0, 0, 0.13);
        border-radius: 6px;
    }

    .table__main_el {
        display: flex;
        justify-content: center;
        width: 100%;
        max-width: 600px;
    }

    .table__el_phone,
    .table__el_name {
        width: 100%;
        width: 300px;
        padding: 24px 64px;
        text-align: center;
        color: var(--text-color);
        font-weight: var(--text-light);
        font-size: 20px;
        white-space: nowrap;
    }

    .table__el_title {
        color: #9f6ad4;
        border-top-left-radius: 6px;
        border-top-right-radius: 6px;
    }

    .bold {
        font-weight: var(--text-weight);
    }

    .table__btn_flex,
    .form__add_btn_flex {
        display: flex;
        justify-content: flex-end;
        margin-top: 64px;
    }

    .table__btn,
    .form__add_btn {
        cursor: pointer;
        background: #ededff;
        padding: 12px 32px;
        text-align: center;
        color: var(--text-color);
        font-weight: var(--text-weight);
        font-size: 18px;
        border-radius: 6px;
        border: none;
    }

    .table__btn:hover,
    .form__add_btn:hover {
        background: #e6e6fc;
    }

    .icon_sort {
        position: absolute;
    }

    .table__el_name_sort {
        cursor: pointer;
    }

    .table__el_name_sort:hover {
        color: #9f6ad4;
    }
</style>
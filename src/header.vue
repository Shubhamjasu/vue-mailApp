<template>
<div class="header">
    <div class="header__left">
        <span class="material-icons" @click="toggleMenu">menu</span>
        <a href="#">
            <img src="src\assets\logo_gmail_lockup_default_1x_r4.png" alt="loading image...." /></a>
    </div>

    <div class="header__middle">
        <span class="material-icons"> search </span>
        <input type="text" placeholder="Search mail" v-model="key" @keyup="keypass" @click="searchBox"/>{{jkey}}
        <span class="material-icons"> arrow_drop_down </span>
    </div>

    <div class="header__right">
        <span class="material-icons"> notifications </span>
        <span class="material-icons"> account_circle </span>
    </div>
</div>
</template>

<script>

import {
    eventBus
} from './main'


export default {
    data() {
        return {
            isOn: true,
            messages: messages,
            key: ''
        }
    },
    props: {
        messages: {
            type: Array,
            required: true
        }
    },
    methods: {
        toggleMenu() {
            this.isOn = !this.isOn,
                eventBus.$emit('toggleMenu', {
                    value: this.isOn
                });
        },
        searchBox() {
            eventBus.$emit('changeView', {
                tag: 'mailsearchresult'
            })
        },
        keypass(){
            eventBus.$emit('searchRes', {
                searchKey : this.key
            });
        }

    },
};
</script>

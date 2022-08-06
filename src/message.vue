<template>
<div v-if="messages.length">
    <div class="emailRow" v-for="(msg, index) in messages" :key="index" @click="openMessage(msg)">
        <div class="emailRow__options">
            <span class="material-icons" v-if="!msg.isImportant"> star_border </span>
            <span class="material-icons" v-if="msg.isImportant"> star </span>
        </div>
        <h3 class="emailRow__title">{{msg.from.email}}</h3>
        <div class="emailRow__message">
            <h4>
                {{msg.subject}}
            </h4>
        </div>
        <p class="emailRow__time">{{msg.date.fromNow()}}</p>
    </div>
</div>
<div v-else class="empty">
<img src="src\assets\no-email-4--no-email-MAIL-MESSAGE-EMPTY-INBOX-DISAPPOINTED-COMMUNICATION-ENVELOPE-SAD-COBWEB-512.webp" alt="loading image">
</div>
</template>
<style>
.empty img{
    height: 50%;
    width: 50%;
}
</style>
<script>
import {
    eventBus
} from './main';

export default {
    props: {
        messages: {
            type: Array,
            required: true
        }
    },
    methods: {
        openMessage(message) {
                eventBus.$emit('changeView', {
                    tag: 'mailmsgcont',
                    data: {
                        message: message
                    }
                });
            }
    }
}
</script>

<template>
<div class="msg-Container">
    <div class="msg-header">
        <h1>New Message</h1>
    </div>
    <form @submit.prevent="sendMessage">
        <div class="msg-caption">
            <input type="email" placeholder="To" v-model="message.to" required>
        </div>
        <div class="msg-title"><input type="text" placeholder="Subject" v-model="message.subject" required></div>
        <div class="message"><textarea v-model="message.content" name="" id="" cols="10" rows="7" required></textarea></div>
        <div>
            <button type="submit">send</button>
        </div>
    </form>
</div>
</template>

<style>
* {
    padding: 0;
    margin: 0;
}

form {
    width: 100%;
    height: 100%;
}

.msg-Container {
    width: 500px;
    border-style: outset;
    border-style: groove;
    border-radius: 5px;
    margin-left: 10%;
    margin-top: 4%;

}

.msg-header {
    background-color: slategray;
    width: 96%;
    height: fit-content;
    color: aliceblue;
    text-align: center;
    font-size: 17px;
    border-radius: 5px;
    padding: 2%;
}



.msg-Container button {
    width: 50%;
    height: 22px;
    margin: auto;
    margin-bottom: 10px;
    margin-left: 25%;

}
.msg-Container button:hover{
    background-color: rgb(32, 142, 226);
    text-decoration: none;
    border-color: aliceblue;
}
.msg-Container div input,
textarea {
    width: 97%;
    height: max-content;
    border: none;
    margin: 1%;
    border-style: groove;
}
</style>

<script>
import moment from 'moment';
import {
    eventBus
} from './main';

export default {
    data() {
        return {
            message: {
                to: '',
                subject: '',
                content: ''
            }
        };
    },
    methods: {
        sendMessage() {
            let previousView = this.$parent.previousView;
            eventBus.$emit('sentMessage', {
                message: {
                    subject: this.message.subject,
                    content: this.message.content,
                    isDeleted: false,
                    type: 'outgoing',
                    date: moment(),
                    from: {
                        name: this.message.to,
                        email: this.message.to
                    },
                    attachments: []
                }
            });
            this.message.subject = '',
                this.message.content = '',
                this.message.to = '',
                eventBus.$emit('changeView', {
                    tag: previousView.tag,
                    title: previousView.title,
                    data: previousView.data
                });
        }

    }
}
</script>

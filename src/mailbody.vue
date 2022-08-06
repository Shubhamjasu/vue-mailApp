<template>
<div id="main">
    <mailsidebar v-if="isOn" :messages="messages"></mailsidebar>
    <keep-alive>
        <component :is="currentView.tag" :data="currentView.data"></component>
    </keep-alive>

</div>
</template>

<script>
import {
    eventBus
} from './main';
import sidebar from './sidebar.vue';
import inbox from './inbox.vue';
import important from './important.vue';
import messageBox from './messageBox.vue';
import searchresult from './searchresult.vue';
import sent from './sent.vue';
import trash from './trash.vue';
import message from './message.vue';
import mescont from './mesCont.vue';

export default {
    data() {
        return {
            isOn: true,
            history: [{
                tag: 'mailinbox',
                data: {
                    messages: null
                }
            }],
        }
    },
    props: {
        messages: {
            type: Array,
            required: true
        }
    },
    components: {

        mailsidebar: sidebar,
        mailinbox: inbox,
        mailimportant: important,
        mailmessagebox: messageBox,
        mailsearchresult: searchresult,
        mailsent: sent,
        mailtrash: trash,
        mailmesssage: message,
        mailmsgcont: mescont
    },
    created() {
        eventBus.$on('changeView', (data) => {
                let temp = [{
                    tag: data.tag,
                    data: data.data || {}
                }];

                this.history = temp.concat(this.history.splice(0));
            }),
            eventBus.$on('toggleMenu', (data) => {
                this.isOn = data.value
            }),
            eventBus.$on('sentMessage', (data) => {
                let temp = [data.message];
                this.messages = temp.concat(this.messages.slice(0));
            });
    },

    computed: {
        currentView() {
            let current = this.history[0];
            current.data.messages = this.messages;
            return current;
        },
        previousView() {
            return typeof this.history[1] !== 'undefined' ? this.history[1] : null;
        }
    }
};
</script>

<style>
#main {
    display: flex;
    flex-direction: row;
}
</style>

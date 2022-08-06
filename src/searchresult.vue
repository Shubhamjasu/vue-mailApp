<template>
<div class="emailList">
    <div class="emailList__settings">
        <div class="emailList__settingsLeft">

        </div>
        <div class="emailList__settingsRight">

        </div>
    </div>

    <div class="emailList__sections">
        <div class="section section__selected">
            <span class="material-icons"> search</span>
            <h4>Search Results</h4>
        </div>

    </div>

    <mailmesssage :messages="resultQuery"></mailmesssage>
</div>
</template>

<script>
import {
    eventBus
} from './main';
import messages from './data/messages';
import message from './message.vue';
export default {
    data() {
        return {
            key: '',
            messages: messages
        }
    },
    created() {
        eventBus.$on('searchRes', (pass) => {
            this.key = pass.searchKey
        })
    },
    components: {
        mailmesssage: message
    },
    computed: {
        resultQuery() {
            if (this.key) {
                return this.messages.filter(item => {
                    return this.key
                        .toLowerCase()
                        .split(" ")
                        .every(v => item.subject.toLowerCase().includes(v));
                });
            } else {
                return this.messages;
            }
        },
        filteredResults() {
            return this.messages.filter(function (mess) {
                return (mess.subject.toLowerCase() == this.key.toLowerCase());
            });
        }
    }
}
// }p.name.toLowerCase().indexOf(this.search.toLowerCase()) != -1;
</script>

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
            <span class="material-icons"> delete </span>
            <h4>Trash</h4>
        </div>

    </div>

   <mailmesssage :messages="trashedMessages"></mailmesssage>
</div>
</template>

<script>
import message from './message.vue';
export default {
    props: {
        data: {
            type: Array,
            required: true
        }
    },
    components: {
        mailmesssage: message
    },
    computed: {
        trashedMessages() {
            return this.data.messages.filter(function (message) {
                return (message.isDeleted === true);
            });
        }
    }
}
</script>

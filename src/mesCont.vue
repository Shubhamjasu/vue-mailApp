<template>
<div class="emailList">
    <div class="emailList__settings">
        <div class="emailList__settingsLeft">
            <span class="material-icons" @click.prevent="navigateBack" > arrow_back </span>
            <span class="material-icons" v-if="!data.message.isDeleted" @click.prevent="data.message.isDeleted = true" v-on:click="navigateBack" :disabled="data.message.isDeleted"> delete </span>
            <span class="material-icons" v-if="!data.message.isImportant && !data.message.isDeleted && data.message.type =='incoming' " @click.prevent="data.message.isImportant = !data.message.isImportant" > star_border </span>
            <span class="material-icons" v-if="data.message.isImportant && !data.message.isDeleted && data.message.type =='incoming' " @click.prevent="data.message.isImportant = !data.message.isImportant" > star </span>
        </div>
    </div>
    <div class="container">
        <div class="msgHeader">
            <p>{{data.message.subject}}</p>
        </div>
        <div class="fromBar">
            <div class="sender" v-if="data.message.type =='incoming'">
                <P >FROM : <br>{{data.message.from.name}} &lt;{{data.message.from.email}}&gt;</P>
            </div>
            <div class="sender" v-if="data.message.type =='outgoing'">
                <div> sent to : <br>{{data.message.from.email}}</div>
            </div>
            <div class="time">{{ data.message.date.fromNow() }}</div>
        </div>
        <div class="content" v-html="data.message.content"></div>
        <!-- <div class="content" v-if="!data.message.isDeleted && data.message.type =='incoming'"><button> Reply</button></div> -->
         
    </div>
</div>
</template>

<style>
.msgHeader {
    font-size: 18px;
    font-weight: 900;
    text-transform: capitalize;
    padding: 1% 2%;
}

.fromBar {
    display: flex;
    flex-direction: row;
    padding: 0% 2%;
    font-size: 11px;
    font-weight: 400;
}

.sender,
.time {
    flex: 50%;
}

.time {
    text-align: right;
}

.content {
    padding: 2%;
    font-size: 14px;
    font-weight: 300;
    line-height: 20px;
}
</style>

<script>
import {
    eventBus
} from './main';

export default {
    props: {
        data: {
            type: Array,
            required: true
        }
    },
    methods: {
            navigateBack() {
                let previousView = this.$parent.previousView;

                eventBus.$emit('changeView', {
                    tag: previousView.tag,
                    title: previousView.title,
                    data: previousView.data
                });
            }
        }
}
</script>

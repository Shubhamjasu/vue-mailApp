<template>
  <div id="app">
  <mailheader :messages="messages"></mailheader>
  <mailbody :messages="messages"></mailbody>
  </div>
</template>

<script>
import header from './header.vue';
import mailbody from './mailbody.vue';
import messages from './data/messages';

export default {
  data() {
    return{
       messages : messages
    }
  },
  components:
  {
    mailheader : header,
    mailbody : mailbody
  }
}
</script>
<style>

</style>

<template>
  <button @click="sendData">Send Data</button>
</template>

<script>
export default {
  name: 'DataSender',

  emits: {
    'sending-start': null,
    'sending-complete': ({ duration, response }) => !!(typeof duration === 'number' && response)
  },

  methods: {
    sendData() {
      this.$emit('sending-start');

      // send data to API

      this.$emit('sending-complete', {
        duration: 2,
        response: 'how are you?'
      });
    }
  }
};
</script>

<style scoped>

</style>

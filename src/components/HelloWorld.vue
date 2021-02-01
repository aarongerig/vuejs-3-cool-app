<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <DataSender
        @sending-start="started"
        @sending-complete="completed"
    />
    <hr>

    <button @click="showMessage = !showMessage">Toggle message</button>
    <button @click="showModal = true">Show modal</button>
    <hr>

    <code>
      <pre>website: {{website}}</pre>
    </code>
    <button @click="addTwitter">Add Twitter</button>
    <button @click="removeLink">Remove link</button>
    <hr>

    Username: {{username}}<br />
    Password: {{password}}<br />
    <LoginForm
      v-model:username="username"
      v-model:password="password"
    />
    <hr>
  </div>

  <teleport to="#modal-container">
    <BaseModal v-if="showModal">
      <h1>Hi Vue School</h1>
      <button @click="showModal = false">Close</button>
    </BaseModal>
  </teleport>

  <teleport to="#purple-box">
    <p v-if="showMessage">Hello from Hello World</p>
  </teleport>
</template>

<script>
import BaseModal from '@/components/BaseModal';
import DataSender from '@/components/DataSender';
import LoginForm from '@/components/LoginForm';
export default {
  name: 'HelloWorld',

  props: {
    msg: String
  },

  components: { BaseModal, DataSender, LoginForm },

  data() {
    return {
      showMessage: true,
      showModal: false,
      website: {
        name: 'Vue School',
        link: 'vueschool.io'
      },
      username: null,
      password: null
    }
  },

  methods: {
    started() {
      console.log('🟢 Started');
    },

    completed({ duration }) {
      console.log(`🏁️ Completed in ${duration} seconds.`);
    },

    addTwitter() {
      this.website.twitter = '@vueschool_io';
    },

    removeLink() {
      delete this.website.link;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

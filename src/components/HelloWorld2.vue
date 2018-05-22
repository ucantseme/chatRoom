<template>
    <div class="borad container">
      <div class="input-group my-5">
        <input type="text" placeholder="輸入暱稱" v-model="username">
        <input type="text" class="form-control" placeholder="請輸入留言內容" v-model="message">
        <div class="input-group-append">
        <button class="btn btn-outline-primary" @click="sendMessage" type="button">Enter</button>
        </div>
      </div>
      <div class="media my-3" v-for="text in messages" >
        <img v-if="text.username != username" class="align-self-start mr-3" src="http://lorempixel.com/80/100">
        <div class="media-body">
          <h3>{{text.username}}</h3>
          <p>{{text.message}}</p>
        </div>
        <img v-if="text.username == username" class="align-self-start mr-3" src="http://lorempixel.com/80/100">
      </div>
  </div>
</template>

<script>
var messagesRef = firebase.database().ref('/messages/')
export default {
  data () {
    return {
      message: '',
      username: '',
      messages: [
        {
          username: 'VueCli',
          message: 'This is Vue-cli!',
        },
        {
          username: 'Justin',
          message: 'Hello!',
        },
      ]
    }
  },
  mounted () {
    let vm = this;
    let messages = [];
      messagesRef.orderByChild("timestamp").on("value",function(snapshot){
        snapshot.forEach(function(msgval){
          messages.unshift(msgval.val());
        })
      });
      vm.messages = messages
  },
  methods:{
    sendMessage () {
      let vm = this;
      let timestamp = Math.floor(Date.now() / 1000);
      messagesRef.child(timestamp).set({
        timestamp: timestamp,
        username: vm.username,
        message: vm.message,
      })
      vm.message = '';
      console.log(messagesRef)
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

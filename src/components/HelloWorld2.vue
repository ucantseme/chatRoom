<template>
    <div class="borad container">
      <div class="input-group my-5">
        <input type="text" class="form-control" placeholder="請輸入留言內容" v-model="message">
        <div class="input-group-append">
        <button class="btn btn-outline-primary" @click="setMessage" type="button">Enter</button>
        </div>
      </div>
      <div class="media my-3" v-for="text in messages" >
        <img v-if="text.username != username" class="align-self-start mr-3" src="https://picsum.photos/80/100">
        <div class="media-body">
          <h3>{{text.username}}</h3>
          <p>{{text.message}}</p>
        </div>
        <img v-if="text.username == username" class="align-self-start mr-3" src="https://picsum.photos/80/100?image=0">
      </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      username: 'VueCli',
      message: '',
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
  methods:{
    setMessage(){
      let vm = this
      vm.messages.unshift({
        username: vm.username,
        message: vm.message,
      })
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

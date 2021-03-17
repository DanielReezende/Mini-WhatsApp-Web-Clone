<template>
  <div id="app">
    <section class="section">
      <div class="container">
        <div class="columns">
          <div class="column is-3 conversation-list">
            <div class="top-bar"></div>
            <item 
              v-for="(conversation, index) in conversations"
              :key="index"
              :activeMessage="index == activeIndex"
              :username="conversation.user"
              :lastMessage="conversation.messages[0].content"
              v-on:click.native="activeIndex=index"
            />
          </div>
          <div class="column active-conversation">
            <div class="top-bar">
              <span>{{ conversations[activeIndex].user }}</span>
            </div>
            <div class="messages-list">
              <message
              v-for="(message, index) in conversations[activeIndex].messages"
              v-bind:key="index" 
              :content="message.content"
              :time="message.time"
              :green="message.green"
            />
            </div>
            <div class="bottom-bar">
              <input type="text" 
              class="input" 
              placeholder="Digite sua mensagem: " 
              v-model="contentNewMessage"
              v-on:keyup.enter="sendMessage"
              >
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import initialData from './data';

// Componentes criados 
import Item from './components/Item';
import Message from './components/Message';

export default {
  data: function(){
    return{
      conversations: initialData,
      activeIndex: 0,
      contentNewMessage: ""
    }
  },
  components:{
    "item": Item,
    "message": Message
  },
  methods: {
    sendMessage: function() {
      let currentTime = new Date().getHours() + ":" + new Date().getMinutes();

      let newMessage = {
        time: currentTime,
        content: this.contentNewMessage,
        green: true
      }

      this.conversations[this.activeIndex].messages.push(newMessage)

      this.contentNewMessage = "";
    }
  }
}
</script>


<style>
  html {
    height: 100vh;
  }
  body{
    background: linear-gradient(180deg, rgba(0,150,136,1) 0%, rgba(0,150,136,1) 15%, rgba(217,219,212,1) 15%);
    min-height: 100vh;
  }

  .columns{
    min-height: 700px;
    box-shadow: 0 3rem 3rem -1rem rgba(10, 10, 10, .2);
  }

  .column{
    padding: 0;
  }

  .conversation-list {
    background: #ffffff;
  }

  .top-bar{
    margin: 0;
    height: 50px;
    background: #ededed;
    border-right: 1px solid #e1e1e1;
    border-bottom: 1px solid rgb(200,200,200);
  }

  .top-bar span {
    line-height: 50px;
    margin-left: 25px;
    font-weight: 500;
  }

  .active-conversation{
    background: #e5ddd5;
  }


  .messages-list {
    height: 80%;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
  }

  .bottom-bar{
    bottom: 0;
    width: 76.5%;
    padding: 10px;
    position: absolute;
    background: #f0f0f0;
  }

  .bottom-bar input {
    border:none;
    padding: 10px;
    margin: 0 50px;
    width: 90%;
    border-radius: 15px;
    font-size: 16px;
  }

</style>
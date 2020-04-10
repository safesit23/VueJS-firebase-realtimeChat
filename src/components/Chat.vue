<template>
  <div class="chat container">
    <h2 class="center teal-text">Simple Chat</h2>

    <div class="card">
      <div class="card-content">
        <ul class="messages" :key="key" v-for="(message, key) in messages">
          <li>
            <span class="teal-text">{{message.name}}</span>
            <span class="gray-text text-darken-3">{{message.content}}</span>
            <span class="gray-text time">{{message.timestamp}}</span>
          </li>
        </ul>
      </div>
      <div class="card-action">
        <NewMessage :name="name" />
      </div>
    </div>
    <!-- <h2>Chat {{ this.name }}</h2> -->
  </div>
</template>

<script>
import NewMessage from "@/components/NewMessage";
import { messages } from "../firebase/config";

export default {
  name: "Chat",
  props: ["name"],
  components: {
    NewMessage
  },
  data() {
    return {
      messages: {}
    };
  },
  created() {
    messages.on("value", snapshot => {
      this.messages = snapshot.val();
    });
    // contactRef.on("value", snapshot => {
    //   this.contacts = snapshot.val();
    // });
  }
};
</script>


<style scoped>
.chat h2 {
  font-size: 2.6;
  margin-bottom: 40px;
}
.chat span {
  font-size: 1.4em;
}
.chat .time {
  display: block;
  font-size: 1.2em;
}
</style>
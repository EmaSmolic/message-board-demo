<template>
  <div class="q-ma-lg">
    <q-input
      standout="bg-teal text-white"
      v-model="title"
      label="Title"
      dense
    ></q-input>
  </div>
  <div class="q-ma-lg">
    <q-input
      standout="bg-teal text-white"
      v-model="text"
      label="Enter the text"
      type="textarea"
    ></q-input>
  </div>
  <div class="q-ma-lg">
    <q-btn @click="sendMessage({ title, text })">Send</q-btn>
  </div>
</template>
<script setup lang="ts">
import { ref } from "vue";
import { Controller } from "src/Classes";

const title = ref("");
const text = ref("");

class MessageController extends Controller {
  public onMessageReceived(message: any): void {
    alert("a message has been received");
  }
}
const demoController = new MessageController(
  "https://test-igrica.onrender.com/"
);
demoController.tryConnecting("pristupni_kod");
const sendMessage = (message: any) => {
  demoController.sendControl(message);
};
</script>

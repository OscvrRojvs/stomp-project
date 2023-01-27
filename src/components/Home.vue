<script setup>
import { Stomp } from "@stomp/stompjs";
import { onMounted, ref } from "vue";
const url = ref("https://api-java-dev.okane.capital/api");
const token = ref(
  "eyJhbGciOiJSUzI1NiIsImtpZCI6ImQwNWI0MDljNmYyMmM0MDNlMWY5MWY5ODY3YWM0OTJhOTA2MTk1NTgiLCJ0eXAiOiJKV1QifQ.eyJuYW1lIjoiT3NjYXIgUm9qYXMiLCJwaWN0dXJlIjoiaHR0cHM6Ly9saDMuZ29vZ2xldXNlcmNvbnRlbnQuY29tL2EvQUFUWEFKd1QwSFBoa1hld1pvdEt6UkdWblJvdlNnRFRKRHhaRk9LWnc0blo9czk2LWMiLCJpc3MiOiJodHRwczovL3NlY3VyZXRva2VuLmdvb2dsZS5jb20vb2thbmUtZGV2LTMwNTgxOCIsImF1ZCI6Im9rYW5lLWRldi0zMDU4MTgiLCJhdXRoX3RpbWUiOjE2NzQ1MDM5MjEsInVzZXJfaWQiOiI3dDNUcHBmNUlQVTNIMzlNbWt4RFpQOEtTYzgyIiwic3ViIjoiN3QzVHBwZjVJUFUzSDM5TW1reERaUDhLU2M4MiIsImlhdCI6MTY3NDgzOTc1NywiZXhwIjoxNjc0ODQzMzU3LCJlbWFpbCI6Im9zY2FyQG9rYW5lLmNhcGl0YWwiLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwiZmlyZWJhc2UiOnsiaWRlbnRpdGllcyI6eyJnb29nbGUuY29tIjpbIjEwNTA2NDU3OTM5NzE2MjgyNTg1OCJdLCJlbWFpbCI6WyJvc2NhckBva2FuZS5jYXBpdGFsIl19LCJzaWduX2luX3Byb3ZpZGVyIjoiZ29vZ2xlLmNvbSJ9fQ.mp0D8ekTLDKZDAQOT0lKHiTbKCO9SsrKi0iDSJD69ZcKwhX5YcvggYPtAu6sHBnX_A47_BUalqRoF-f5kaL5uUCwfJptP1LqbydlynAdCKwvHVGFQ7e1EbAvxwZBIXNzlmxgZBI7wMyzB6ekPXhYxQr1gufTzUm6j-jKWmB9bxe7jZ52oqD6pJZ9u0BVotJ28uV7TiO7hWaeHD61yAPwfTdKHJtcalBbpgw67LXETnjVZ2wgbfzBgg-LNW3EgnfXDGFgAnE0AJbJbvaORATwyjPa_YT-tkXyON6vCfbmNiXlco0QopBwMMN7GjyHGa1A7VhwznthXKrjeW1xp_HLZg"
);
const topic = ref("TM_ORDER");
const messages = ref([]);
const disabledButton = ref(true);
let stompClient = Stomp.over(function () {
  return new SockJS(url.value);
});

onMounted(() => {
  connect();
});

const connect = () => {
  stompClient.connect({}, async (frame) => {
    console.log("[STOMP SOCKET] - CONNECTED");
    disabledButton.value = false;
  });
};
const suscribeOrders = () => {
  stompClient.send(
    `${url.value}/modules/trademonitor/subscribe`,
    {},
    JSON.stringify({
      topic: "TM_ORDER",
      authorization:
        "eyJhbGciOiJSUzI1NiIsImtpZCI6ImQwNWI0MDljNmYyMmM0MDNlMWY5MWY5ODY3YWM0OTJhOTA2MTk1NTgiLCJ0eXAiOiJKV1QifQ.eyJuYW1lIjoiT3NjYXIgUm9qYXMiLCJwaWN0dXJlIjoiaHR0cHM6Ly9saDMuZ29vZ2xldXNlcmNvbnRlbnQuY29tL2EvQUFUWEFKd1QwSFBoa1hld1pvdEt6UkdWblJvdlNnRFRKRHhaRk9LWnc0blo9czk2LWMiLCJpc3MiOiJodHRwczovL3NlY3VyZXRva2VuLmdvb2dsZS5jb20vb2thbmUtZGV2LTMwNTgxOCIsImF1ZCI6Im9rYW5lLWRldi0zMDU4MTgiLCJhdXRoX3RpbWUiOjE2NzQ1MDM5MjEsInVzZXJfaWQiOiI3dDNUcHBmNUlQVTNIMzlNbWt4RFpQOEtTYzgyIiwic3ViIjoiN3QzVHBwZjVJUFUzSDM5TW1reERaUDhLU2M4MiIsImlhdCI6MTY3NDgzOTc1NywiZXhwIjoxNjc0ODQzMzU3LCJlbWFpbCI6Im9zY2FyQG9rYW5lLmNhcGl0YWwiLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwiZmlyZWJhc2UiOnsiaWRlbnRpdGllcyI6eyJnb29nbGUuY29tIjpbIjEwNTA2NDU3OTM5NzE2MjgyNTg1OCJdLCJlbWFpbCI6WyJvc2NhckBva2FuZS5jYXBpdGFsIl19LCJzaWduX2luX3Byb3ZpZGVyIjoiZ29vZ2xlLmNvbSJ9fQ.mp0D8ekTLDKZDAQOT0lKHiTbKCO9SsrKi0iDSJD69ZcKwhX5YcvggYPtAu6sHBnX_A47_BUalqRoF-f5kaL5uUCwfJptP1LqbydlynAdCKwvHVGFQ7e1EbAvxwZBIXNzlmxgZBI7wMyzB6ekPXhYxQr1gufTzUm6j-jKWmB9bxe7jZ52oqD6pJZ9u0BVotJ28uV7TiO7hWaeHD61yAPwfTdKHJtcalBbpgw67LXETnjVZ2wgbfzBgg-LNW3EgnfXDGFgAnE0AJbJbvaORATwyjPa_YT-tkXyON6vCfbmNiXlco0QopBwMMN7GjyHGa1A7VhwznthXKrjeW1xp_HLZg",
    })
  );
  let subscription = stompClient.subscribe(
    `/topic/oscar/trademonitor/orders`,
    (message) => {
      const orderReply = JSON.parse(message.body);
      const { operation, order } = orderReply;
      messages.value.push(operation);
      messages.value.push(order);
      console.log(operation, order);
    }
  );
};
</script>

<template>
  <v-container>
    <h1>stomp js</h1>
    <v-row no-gutters>
      <v-col cols="6"
        ><v-row
          ><v-col class="pa-5" cols="12">
            <v-text-field
              v-model="url"
              label="URL"
              hide-details="auto"
            ></v-text-field>
          </v-col>
          <v-col class="pa-5" cols="12">
            <v-text-field
              v-model="token"
              label="Token"
              hide-details="auto"
            ></v-text-field>
          </v-col>
          <v-col class="pa-5" cols="12">
            <v-text-field
              v-model="topic"
              label="Topic"
              hide-details="auto"
            ></v-text-field>
          </v-col>
          <v-col class="pa-5" cols="12">
            <v-btn @click="suscribeOrders"> suscribirse </v-btn>
          </v-col></v-row
        ></v-col
      >
      <v-col cols="6"
        ><p v-for="msg in messages" :key="msg.id">{{ msg }}</p></v-col
      >
    </v-row>
  </v-container>
</template>

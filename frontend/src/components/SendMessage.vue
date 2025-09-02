<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gray-100">
    <div class="w-full max-w-md bg-white p-6 rounded-2xl shadow-lg">
      <h2 class="text-xl font-bold mb-4 text-center text-blue-600">Enviar Mensaje</h2>
      <input
        v-model="message"
        type="text"
        placeholder="Escribe tu mensaje..."
        class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-400"
      />
      <button
        @click="sendMessage"
        class="w-full mt-4 px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition"
      >
        Enviar
      </button>
      <p v-if="response" class="mt-4 text-green-600 font-medium">{{ response }}</p>
      <p v-if="error" class="mt-4 text-red-600 font-medium">{{ error }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "MessageSender",
  data() {
    return {
      message: "",
      response: null,
      error: null,
    };
  },
  methods: {
    async sendMessage() {
      this.response = null;
      this.error = null;
      try {
        const res = await axios.post(
          process.env.VUE_APP_API_URL,
          { message: this.message }
        );
        this.response = "Mensaje enviado correctamente"+ JSON.stringify(res.data);
        this.message = "";
      } catch (err) {
        this.error = "Error al enviar mensaje"
        console.log(err);
      }
    },
  },
};
</script>

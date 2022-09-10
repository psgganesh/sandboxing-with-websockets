<template>
  <div class="flex flex-col h-screen bg-[url('./assets/memphis-colorful.png')]">
    <div class="flex-grow bg-pattern">
      <div class="section h-full">
        <ol class="h-full flex flex-col justify-end align-bottom p-2">
          <li
              v-for="(message, index) in messages"
              :key="index"
              class="rounded border-2 border-gray-50 p-2 my-2 bg-amber-50"
          >
            {{ message.text }}
          </li>
        </ol>
      </div>
    </div>
    <div class="border-x-0 border-solid border-slate-500 border-t-2 border-b-0 bg-white">
      <div class="flex rounded-md shadow-sm">
        <div class="relative flex items-stretch flex-grow focus-within:z-10 p-5">
          <input
              type="text"
              class="focus:outline-none block w-full pl-2 sm:text-md bg-white"
              placeholder="Send your message ..."
              v-model="input"
              @keydown.enter="send"
          />
        </div>
        <button
            type="button"
            @click="send"
            class="inline-flex items-center px-5 py-2 border border-transparent shadow-sm text-gray-900 bg-green-50 hover:bg-green-100 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-green-100"
        >
          <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 512 512"
              class="h-5 w-5 mr-2"
              stroke="current-color"
          >
            <path
                d="M511.6 36.86l-64 415.1c-1.5 9.734-7.375 18.22-15.97 23.05c-4.844 2.719-10.27 4.097-15.68 4.097c-4.188 0-8.319-.8154-12.29-2.472l-122.6-51.1l-50.86 76.29C226.3 508.5 219.8 512 212.8 512C201.3 512 192 502.7 192 491.2v-96.18c0-7.115 2.372-14.03 6.742-19.64L416 96l-293.7 264.3L19.69 317.5C8.438 312.8 .8125 302.2 .0625 289.1s5.469-23.72 16.06-29.77l448-255.1c10.69-6.109 23.88-5.547 34 1.406S513.5 24.72 511.6 36.86z"
            />
          </svg>
          <span>Send</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: "",
      messages: [],
      socketConnection: null,
    }
  },
  mounted() {
    // Calling onconnect Lambda function via API endpoint
    const instance = this;
    const connection = new WebSocket(import.meta.env.VITE_WEB_SOCKET_API_ENDPOINT);
    this.socketConnection = connection;
    connection.onopen = function (e) {
      console.log("onopen");
      console.dir(e);
    };
    connection.onerror = function (error) {
      console.error("onerror");
      console.dir(error);
    };
    connection.onmessage = function (e) {
      console.log("onmessage");
      console.dir(e);
      if (e && e.data) {
        instance.messages.push({ text: e.data });
      }
    };
    connection.onclose = function () {
      console.log("onclose");
    };
  },
  methods: {
    // Calling sendmessage Lambda function via API endpoint
    send: function () {
      this.socketConnection.send(
          JSON.stringify({
            action: "onsend",
            data: this.input,
          })
      );
      this.input = "";
    },
    disconnect: function () {
      // Calling ondisconnect Lambda function via API endpoint
      this.socketConnection.disconnect();
    },
  },
}
</script>
<script>
export default {
  data() {
    return {
      socketConnection: null,
      isValidSocketConnection: false
    }
  },
  mounted() {
    this.socketConnection = import.meta.env.VITE_WEB_SOCKET_API_ENDPOINT
    this.isValidSocketConnection = this.socketConnection.includes('wss://')
  }
}
</script>

<template>
  <div class="relative flex min-h-screen flex-col justify-center overflow-hidden bg-gray-50 py-6 sm:py-12">
    <img src="./assets/beams.jpeg" alt="background-image" class="absolute top-1/2 left-1/2 max-w-none -translate-x-1/2 -translate-y-1/2" width="1308" />
    <div class="relative bg-white px-6 pt-10 pb-8 shadow-xl ring-1 ring-gray-900/5 sm:mx-auto sm:max-w-lg sm:rounded-lg sm:px-10">
      <div class="mx-auto max-w-md">
        <div class="divide-y divide-gray-300/50">
          <div class="space-y-6 py-8 text-base leading-7 text-gray-600">
            <ul class="space-y-4">
              <li class="flex items-center">
                <svg class="h-6 w-6 flex-none fill-green-100 stroke-green-500 stroke-2" stroke-linecap="round" stroke-linejoin="round">
                  <circle cx="12" cy="12" r="11" />
                  <path d="m8 13 2.165 2.165a1 1 0 0 0 1.521-.126L16 9" fill="none" />
                </svg>
                <p class="ml-4">
                  Frontend tools are setup
                </p>
              </li>
              <li class="flex items-center" v-if="isValidSocketConnection">
                <svg class="h-6 w-6 flex-none fill-green-100 stroke-green-500 stroke-2" stroke-linecap="round" stroke-linejoin="round">
                  <circle cx="12" cy="12" r="11" />
                  <path d="m8 13 2.165 2.165a1 1 0 0 0 1.521-.126L16 9" fill="none" />
                </svg>
                <p class="ml-4">
                  Websocket URI is set in the .env file
                </p>
              </li>
              <li class="flex items-center" v-else>
                <svg class="h-7 w-7 text-red-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.28 7.22a.75.75 0 00-1.06 1.06L8.94 10l-1.72 1.72a.75.75 0 101.06 1.06L10 11.06l1.72 1.72a.75.75 0 101.06-1.06L11.06 10l1.72-1.72a.75.75 0 00-1.06-1.06L10 8.94 8.28 7.22z" clip-rule="evenodd" />
                </svg>
                <p class="ml-4">
                  <code class="text-sm font-bold text-red-500">Websocket URI is not set in the .env file</code>
                </p>
              </li>
            </ul>
            <p>Perfect now you can continue to Step 3 to create an app with Chat UI</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


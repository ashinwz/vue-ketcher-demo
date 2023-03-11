<template>
  <div class="px-4 py-4">
    <p style="font-size: 14px">Click the button below to activate ketcher</p>
    <button @click="isOpen = true" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
      <BoltIcon
        class="h-4 w-4 text-white "
        aria-hidden="true"
      />
    </button>
    <p style="font-size: 14px">Mol SMILES is : {{ ketcherSmiles}}</p>

    <div v-if="isOpen" class="fixed inset-0 overflow-y-auto">
      <div class="flex items-center justify-center min-h-screen p-4">
        <div class="bg-white rounded-lg shadow-lg p-4 z-10">
          <div class="mb-4">
            <h2 class="text-lg font-bold">{{ title }}</h2>
            <p class="text-sm text-gray-500">{{ message }}</p>
          </div>
          <div class="modal-body">
            <iframe class="frame" id="idKetcher" src="./standalone/index.html" width="800" height="550" />
          </div>
          <div class="flex justify-center items-center text-right mt-4">
            <button @click="getSmiles" class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded mr-2">
                Save
            </button>
            <button @click="isOpen = false" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
              Close
            </button>

          </div>
        </div>
      </div>
      <div class="fixed inset-0 bg-gray-700 bg-opacity-75"></div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import { BoltIcon } from "@heroicons/vue/20/solid";

export default {
  name: 'MyModal',
  components: {
    BoltIcon
  },
  setup(props) {
    const isOpen = ref(false)
    const ketcherSmiles = ref(null)
    const title = ref('Ketcher Sketcher')
    const message = ref('Designed for chemists, laboratory scientists and technicians who draw structures and reactions.')

    return {
      isOpen,
      title,
      message,
      ketcherSmiles
    }
  },
  methods: {
    getSmiles() {
      this.initKetcher()
      this.ketcher
        .getSmiles()
        .then(res => {
          this.ketcherSmiles = res
          this.isOpen = false
        })
        .catch(e => {
          console.log(e)
        })
    },
    initKetcher() {
      let ketcherFrame = document.getElementById('idKetcher')
      let ketcher = null
      if ('contentDocument' in ketcherFrame) {
        ketcher = ketcherFrame.contentWindow.ketcher
      } else {
        ketcher = document.frames['idKetcher'].window.ketcher
      }
      this.ketcher = ketcher
    },
  }
};
</script>

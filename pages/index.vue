<template>
  <div>
    <header class="shadow-sm bg-white">
      <div class="container mx-auto p-4 m-4 flex justify-between">
          <strong class="w-1/6 text-lg"><b>RedComm Sticky Note</b></strong>
          <button @click="$fetch" class="w-1/6 justify-center text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800">Refresh</button>
          <button id="button" data-modal-toggle="modal" data-modal-target="modal" type="button" class="w-1/6 justify-center text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg px-5 py-2.5 mr-2 text-sm dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800">Add</button>
          <!--Search Start -->
          <div class="flex items-center w-3/6">   
              <label for="simple-search" class="sr-only">Search</label>
              <div class="relative w-full">
                  <div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
                      <svg aria-hidden="true" class="w-5 h-5 text-gray-500 dark:text-gray-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z" clip-rule="evenodd"></path></svg>
                  </div>
                  <input type="text" v-model="searchInput" id="simple-search" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full pl-10 p-2.5  dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Search" required>
              </div>
              <button type="button" @click="search" class="p-2.5 ml-2 text-sm font-medium text-white bg-blue-700 rounded-lg border border-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
                  <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path></svg>
                  <span class="sr-only">Search</span>
              </button>
          </div>
          <!--Search End -->
        </div>
      </header>

      <!-- Modal Start -->
      <div id="modal" tabindex="-1" aria-hidden="true" class="fixed top-0 left-0 right-0 z-50 hidden w-full p-4 overflow-x-hidden overflow-y-auto md:inset-0 h-[calc(100%-1rem)] max-h-full">
          <div class="relative w-full max-w-2xl max-h-full">
              <!-- Modal content -->
              <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
                  <!-- Modal header -->
                  <div class="flex items-start justify-between p-5 border-b rounded-t dark:border-gray-600">
                      <h3 class="text-xl font-semibold text-gray-900 lg:text-2xl dark:text-white">
                          Create New Note
                      </h3>
                      <button id="closeButton" data-modal-hide="modal" type="button" class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm p-1.5 ml-auto inline-flex items-center dark:hover:bg-gray-600 dark:hover:text-white">
                          <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>  
                      </button>
                  </div>
                  <!-- Modal body -->
                    <div class="mb-12 p-4">
                      <input v-model="title" placeholder="Title" class="pblock w-full p-4 mb-4 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-md focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
	                    <textarea v-model="desc" placeholder="Desc" class="block w-full p-4 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-md focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"></textarea>
                    </div>
                  

                  <!-- Modal footer -->
                    <div class="flex items-center p-6 space-x-2 border-t border-gray-200 rounded-b dark:border-gray-600">
                        <button id="addNote" type="button" @click="addNote" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"><i class="fas fa-address-card"></i>Add</button>
                        <button id="cancelAdding" data-modal-hide="modal" type="button" class="text-gray-500 bg-white hover:bg-gray-100 focus:ring-4 focus:outline-none focus:ring-blue-300 rounded-lg border border-gray-200 text-sm font-medium px-5 py-2.5 hover:text-gray-900 focus:z-10 dark:bg-gray-700 dark:text-gray-300 dark:border-gray-500 dark:hover:text-white dark:hover:bg-gray-600">Cancel</button>
                    </div>
              </div>
          </div>
      </div>
      <!-- Modal End -->

      <!-- Fetch Data -->
      <div>
        <p v-if="$fetchState.pending">Fetching mountains...</p>
        <p v-else-if="$fetchState.error">An error occurred</p>
        <div v-else>
          <div class="grid grid-cols-2 gap-5 m-4">
            <div v-for="product of products" class="card p-4">
              <h1><b class="text-left">{{ product.title }}</b> <button class="btn float-right">DEL</button></h1>
              <p>{{ product.description }}</p>
            </div>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
//import for modal
import { onMounted } from 'vue'
import { Modal } from 'flowbite'

export default {
  //init data
  data() {
	  return {
    	title: '',
      desc: '',
      searchInput: '',
      products:[]
  	}
	},
  //fetch data from API
  async fetch() {
    this.products = await fetch(
      'https://fakestoreapi.com/products'
    ).then(res => res.json())
  },
  //Add and Search
  methods: {
    addNote(event) {
      // `this` inside methods points to the current active instance
      alert(`Hello ${this.title} and ${this.desc}!`)
      // `event` is the native DOM event
    },
    search(event){
      alert(`Search Input: ${this.searchInput}`)
    }
  },
}



onMounted(() => {
    
    // setup available elements
    const $buttonElement = document.querySelector('#button');
    const $modalElement = document.querySelector('#modal');
    const $closeButton = document.querySelector('#closeButton');
    const $cancelAdding = document.querySelector('#cancelAdding');

    // set modal options
    const modalOptions = {
        backdropClasses: 'bg-gray-900 bg-opacity-50 dark:bg-opacity-80 fixed inset-0 z-40'
    }

    // create a new modal instance
    if ($modalElement) {
        const modal = new Modal($modalElement, modalOptions);

        // set event listeners for the button to show the modal
        $buttonElement.addEventListener('click', () => modal.toggle());
        $closeButton.addEventListener('click', () => modal.hide());
        $cancelAdding.addEventListener('click', () => modal.hide());
    }
})
</script>

<style>
  .btn {
    @apply bg-blue-600 text-white px-3 py-2 rounded-md text-sm;
  }
  .card {
    @apply p-3 rounded-md bg-white shadow-md h-full;
  }
    </style>
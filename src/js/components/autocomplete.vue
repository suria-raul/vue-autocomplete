<template>
  <div class="autocomplete flex flex-col items-center">
    <h1 class="h1 text-center">Autocomplete</h1>
    <div class="absolute inset-0 z-0" @click="modal = false"></div>
    <input 
      type="text"
      v-model="state"
      class="bg-gray-900 mx-auto mt-10 block text-white px-4 py-2 z-10"
      autocomplete="off"
      @focus="modal = true">

    <div v-if="filteredStates && modal" class="z-10">
      <ul class="w-64 bg-gray-800 text-white">
        <li v-for="filteredState in filteredStates" class="px-4 py-2 border-b cursor-pointer" @click="setState(filteredState)">
          {{ filteredState }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        state: '',
        states: [
          'Alabama',
          'Florida',
          'Alaska',
          'Texas',
          'Vermont',
          'California',
          'New Jersey',
          'Virginia'
        ],
        filteredStates: [],
        modal: false,
      }
    },

    methods: {
      setState(filteredState) {
        this.state = filteredState
        this.modal = false
      }
    },

    watch: {
      state() {
        this.filteredStates = this.states.filter(state => {
          return state.toLowerCase().startsWith(this.state.toLowerCase())
        })
      }
    }
  }
</script>
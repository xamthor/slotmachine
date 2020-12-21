<template>

	<button @click="darkThemeSwitch"
        type="button"
        class="border border-gray-700 text-gray-700 rounded-md px-4 py-2 m-2 transition duration-500 ease select-none hover:text-white hover:bg-gray-800 focus:outline-none focus:shadow-outline absolute top-0 right-0 

        dark:text-white dark:border-white"
        >
          Toggle
        </button>

	<slotMachine />
</template>

<script>
import slotMachine from "./components/slotMachine.vue";

export default {
	name: "App",
	components: {
	slotMachine
	},
	data() {
		return{
		mode: localStorage.theme
		}
	},
	mounted() {
        console.log('Component mounted.')
        document.querySelector('html').classList.toggle(this.mode)
    },

	methods: {
		darkThemeSwitch() {

		document.querySelector('html').classList.toggle('dark')

		if (document.querySelector('html').classList.contains('dark')) 
		{
			localStorage.theme = 'dark'
		}else
		{
			localStorage.theme = 'light'
		}
		


		}

	}
};
</script>

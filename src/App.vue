<template>
	<devices />
	<burger @toggleBurger="openBurger" ref="burger"/>
	<sidebar :isOpen="isBurgerOpen" @openPage="loadPage" :menu="menu" />
	<page :pageContent="currentPage" ref="page" />
</template>

<script>
import Devices from './Devices.vue'
import Burger from './Burger.vue'
import Sidebar from './Sidebar.vue'
import Page from './Page.vue'

export default {
	name: 'App',
	components: {
		Devices,
		Burger,
		Sidebar,
		Page,
	},
	data() {
		return {
			menu: [],
			currentPage: {},
			isBurgerOpen: false,
		}
	},
	methods: {
		openBurger(toggle) {
			this.isBurgerOpen = toggle
		},
    loadPage(id) {
      this.currentPage = this.menu.find(page => page.id == id)['content']
      this.$refs.burger.toggle()
      this.$refs.page.isFullText = false
    }
	},
	async created() {
		try {
			const response = await fetch('site.json', {
				headers: {
					'Content-Type': 'application/json',
					Accept: 'application/json',
				},
			})
			const data = await response.json()
			let set = new Set()
			this.menu = data.menu.filter(obj => set.size !== set.add(obj.id).size)
			this.currentPage = this.menu.find(page => page.id == 1)['content']
		} catch (e) {
			console.log(e)
		}
	},
}
</script>

<style>
body {
	padding: 0;
	margin: 0;
	font-family: 'Roboto', sans-serif;
	font-size: 1.25rem;
}
</style>

<template>
	<devices />
	<burger @toggleBurger="openBurger" ref="burger" />
	<sidebar :isOpen="isBurgerOpen" @openPage="loadPage" :menu="data" />
	<page :pageContent="currentPage" ref="page" />
</template>

<script>
import { computed, ref } from 'vue'
import { swr } from './swr.js'
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
	setup() {
		const cache = swr(
			'menu',
			fetch('site.json')
				.then(response => response.json()),
			[]
		)
		const isLoading = computed(() => !cache.data.menu.length && cache.isRevalidating)
		const isError = computed(() => cache.isError)
		const error = computed(() => cache.error)
		const data = computed(() => {
			let set = new Set()
			return cache.data.menu.filter(obj => set.size !== set.add(obj.id).size)
		})
		let currentPage = ref(data.value.find(page => page.id == 1)['content'])
		let isBurgerOpen = ref(false)

		const burger = ref()
		const page = ref()

		function openBurger(toggle) {
			isBurgerOpen.value = toggle
		}

		function loadPage(id) {
			currentPage.value = data.value.find(page => page.id == id)['content']
			burger.value.toggle()
			page.value.isFullText = false
		}

		return { isLoading, isError, error, data, currentPage, isBurgerOpen, openBurger, loadPage, burger, page }
	}
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

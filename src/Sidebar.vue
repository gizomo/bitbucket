<template>
	<div class="sidebar">
		<transition name="slide">
			<div v-if="isOpen" class="sidebar-panel">
				<ul class="sidebar-panel-nav">
					<li
						class="menu-item"
						v-for="page in menu"
						:key="page.id"
						@click="openPage(page.id)"
					>
						<span class="menu-item--title">{{ page.menu_title }}</span>
						<i class="material-icons">arrow_forward_ios</i>
					</li>
				</ul>
			</div>
		</transition>
	</div>
</template>
<script>
export default {
	props: {
		menu: {
			type: Array,
		},
		isOpen: {
			type: Boolean,
			default: false,
		},
	},
	methods: {
		openPage(id) {
			this.$emit('openPage', id)
		},
	},
}
</script>
<style scoped>
.sidebar {
	position: relative;
	z-index: 10;
}
.sidebar-panel {
	overflow-y: auto;
	position: fixed;
	left: 0;
	top: 0;
	height: 100vh;
	min-width: 240px;
	padding-top: 3rem;
	color: #fff;
	background-color: #35434c;
	border-left: 2px solid #f97252;
}
.sidebar-panel-nav {
	padding: 0;
	margin: 0;
	list-style-type: none;
	cursor: pointer;
}
.menu-item {
	display: flex;
	justify-content: space-between;
	align-items: center;
	color: #fff;
	padding: 1rem;
	border-bottom: 1px solid #35434c;
	background-color: #2c3941;
}
.menu-item:hover {
  background-color: #2c2c2c;
}
.slide-enter-active,
.slide-leave-active {
	transition: transform 0.2s ease;
}

.slide-enter,
.slide-leave-to {
	transform: translateX(-100%);
	transition: all 150ms ease-in 0s;
}
</style>

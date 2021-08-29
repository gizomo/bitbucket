<template>
	<div class="devices">
		<i class="material-icons" :class="{ active: isMobile }"
			>smartphone</i
		>
		<i class="material-icons" :class="{ active: isTablet }"
			>tablet_mac</i
		>
		<i
			class="material-icons"
			:class="{ active: !isMobile && !isTablet }"
			>desktop_mac</i
		>
	</div>
</template>
<script>
import { isMobileOnly, isTablet } from 'mobile-device-detect'

export default {
	name: 'App',
	data() {
		return {
			isMobile: isMobileOnly,
			isTablet: isTablet,
		}
	},
}
</script>
<style lang="less" scoped>
.devices {
	position: fixed;
	left: 0;
	right: 0;
	display: flex;
	justify-content: center;
	background-color: #fff;
	z-index: 2;
	i {
		padding: 1rem;
	}
}
.active {
	background-color: #ebebeb;
}
</style>

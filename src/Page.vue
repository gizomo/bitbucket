<template>
	<div class="page">
		<div class="page-content">
			<div
				class="page-content--image"
				:class="{ minimized: !pageContent.image_url }"
				:style="{ backgroundImage: 'url(' + pageContent.image_url + ')' }"
			></div>
			<div class="page-content--text">
				<div class="page-title">{{ pageContent.header }}</div>
				<div class="page-summary" v-if="!isFullText">
					{{ pageContent.short_text }}
				</div>
				<div class="page-full-text" v-if="isFullText">
					{{ pageContent.full_text }}
				</div>
				<button
					class="page-button"
					v-if="!isFullText && pageContent.full_text && pageContent.full_text_btn_title"
					@click.prevent="openPage"
				>
					{{ pageContent.full_text_btn_title }}
				</button>
			</div>
		</div>
	</div>
</template>
<script>
export default {
	props: {
		pageContent: {
			type: Object,
		},
	},
	data() {
		return {
			isFullText: false,
		}
	},
	methods: {
		openPage() {
			this.isFullText = !this.isFullText
		},
	},
}
</script>
<style scoped>
.page {
	min-height: 100vh;
	width: 100%;
	display: flex;
	align-items: center;
	color: #fff;
	background-color: #f97252;
}
.page-content {
	width: 100%;
	padding: 3.5rem;
	display: flex;
	justify-content: space-between;
	gap: 3.5rem;
}
.page-content--image {
	flex: 1;
	height: 50vh;
	background-size: cover;
	background-position: center;
}
.minimized {
	height: auto;
}
.page-content--text {
	flex: 1;
}
.page-title {
	margin: 1rem 0;
	text-transform: uppercase;
	letter-spacing: 0.5rem;
	font-size: 2.5rem;
	font-weight: 700;
}
.page-summary,
.page-full-text {
	margin: 2.5rem 0;
}
.page-button {
	padding: 1rem 1.5rem;
	text-transform: uppercase;
	letter-spacing: 0.15rem;
	border: 2px solid #fff;
	color: #fff;
	background-color: #f97252;
	box-shadow: none;
	cursor: pointer;
	transition: all 0.3s ease;
	position: relative;
}

.page-button {
	overflow: hidden;
	transition: all 0.3s ease;
}
.page-button:hover {
	filter: saturate(0.2);
	color: #fff;
}
.page-button:hover::before {
	position: absolute;
	content: '';
	display: inline-block;
	top: -180px;
	left: 0;
	width: 30px;
	height: 100%;
	background-color: #fff;
	animation: shiny-btn 3s ease-in-out infinite;
}
.page-button:active {
	box-shadow: 4px 4px 6px 0 rgba(255, 255, 255, 0.3),
		-4px -4px 6px 0 rgba(116, 125, 136, 0.2),
		inset -4px -4px 6px 0 rgba(255, 255, 255, 0.2),
		inset 4px 4px 6px 0 rgba(0, 0, 0, 0.2);
}

@-webkit-keyframes shiny-btn {
	20% {
		-webkit-transform: scale(0) rotate(45deg);
		opacity: 0;
	}
	60% {
		-webkit-transform: scale(0) rotate(45deg);
		opacity: 0.5;
	}
	61% {
		-webkit-transform: scale(4) rotate(45deg);
		opacity: 1;
	}
	100% {
		-webkit-transform: scale(50) rotate(45deg);
		opacity: 0;
	}
}

@media screen and (max-width: 40em) {
	.page-content {
		display: block;
		padding: 2rem;
	}
}
</style>

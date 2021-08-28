<template>
	<div class="page">
		<div class="page-image" :style="{ backgroundImage: 'url(' + pageContent.image_url + ')' }"></div>
		<div class="page-content">
			<div class="page-title">{{ pageContent.header }}</div>
			<div class="page-summary" v-if="!isFullText">{{ pageContent.short_text }}</div>
			<div class="page-full-text" v-if="isFullText">{{ pageContent.full_text }}</div>
			<button class="page-button" v-if="!isFullText" @click.prevent="openPage">
				{{ pageContent.full_text_btn_title }}
			</button>
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
      isFullText: false
    }
  },
  methods: {
    openPage() {
      this.isFullText = !this.isFullText
    }
  }
}
</script>
<style scoped>
.page {
  padding: 3rem;
  min-height: 100vh;
  display: flex;
  justify-content: space-around;
  align-items: center;
  gap: 2rem;
	color: #fff;
	background-color: #f97252;
}
.page-image {
  width: 50vw;
  height: 50vh;
  background-size: cover;
  background-position: center;
}
.page-title {
  margin: 1rem 0;
  font-size: 2rem;
  font-weight: 700;
}
.page-summary, .page-full-text {
  margin: 1rem 0;
}
.page-button {
  padding: 0.5rem 1rem;
  border: 2px solid #fff;
  color: #fff;
  background-color: #f97252;
  box-shadow: none;
}


@media screen and (max-width: 40em) {
  .page{
    display: block;
  }
}
</style>
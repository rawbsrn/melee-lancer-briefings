<template>
	<div class="pilot-modal">
		<div class="pilot-header-container">
			<div class="section-header clipped-medium-backward-bio">
				<img src="/icons/pilot-icon.svg" />
				<h1>{{ guest.alias }} [{{ guest.callsign }}]</h1>
			</div>
			<div class="rhombus-back">&nbsp;</div>
		</div>
		<div class="pilot">
			<Markdown :source="bio" class="markdown" />
		</div>
	</div>
	<div class="pilot-modal portrait">
		<div class="pilot-header-container">
			<div class="section-header clipped-medium-backward-pilot">
				<img src="/icons/portrait-icon.svg" />
				<h1>guest Artwork</h1>
			</div>
			<div class="rhombus-back">&nbsp;</div>
		</div>
		<div class="pilot">
			<img :src="portrait" class="portrait" />
		</div>
	</div>
</template>

<script>
import Markdown from 'vue3-markdown-it';

export default {
	components: {
		Markdown
	},
	data() {
		return {
			bio: "",
		}
	},
	props: {
		guest: {
			type: Object,
			required: true,
		}
	},
	computed: {
		portrait() {
			return `/guests/${this.guest.callsign}.png`
		},
	},
	created() {
		let self = this;
		let md = `/guests/${this.guest.callsign}.md`
		var client = new XMLHttpRequest();
		client.open('GET', md);
		client.onreadystatechange = function () {
			self.bio = client.responseText;
		}
		client.send();
	},
	methods: {

	}
}
</script>
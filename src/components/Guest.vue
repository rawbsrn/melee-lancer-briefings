<template>
	<div class="pilot-wrapper" @click="guestModal">
		<div class="pilot">
			<img :src="guestPortrait" class="pilot-portrait" />
			<div class="pilot-loadout">
				<div class="name">
					<h1>Callsign</h1>
					<h2>{{ guest.callsign }}</h2>
				</div>
				<div class="name">
					<h1>Name or Legal Alias</h1>
					<h2>{{ guest.alias }}</h2>
				</div>
				<div class="code">{{ guest.code }}</div>
			</div>
			<div class="mech-loadout">
				<div class="name">
					<h1>{{ guest.corpro }} // {{ guest.frame }}</h1>
					<h2>{{ guest.mech }}</h2>
				</div>
			</div>
		</div>
		<div class="middle">
			<div class="text">&nbsp;</div>
		</div>
	</div>
</template>

<script>

import guestModal from './GuestModal.vue';

export default {
	components: {
		guestModal
	},
	props: {
		guest: {
			type: Object,
			required: true,
		}
	},
	computed: {
		guestPortrait() {
			return `/guests/${this.guest.callsign}.png`
		},

	},
	methods: {
		guestModal() {
			this.$oruga.modal.open({
				parent: this,
				component: guestModal,
				custom: true,
				trapFocus: true,
				props: {
					guest: this.guest,
				},
				class: "TEST",
				width: 1920,
			});
		},
	}
}
</script>
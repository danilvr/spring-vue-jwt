<template>
	<v-snackbar
		v-model="show"
		:color="color"
		:top="top"
		right
	>
		{{ message }}

		<template v-slot:action="{ attrs }">
			<v-btn
				text
				v-bind="attrs"
				@click="show = false"
			>
				Close
			</v-btn>
		</template>
	</v-snackbar>
</template>

<script>
	export default {
		name: 'Snackbar',
		data: () => ({
			show: false,
			message: '',
			color: '',
		}),
		created() {
			this.$store.subscribe((mutation, state) => {
				if (mutation.type === 'snackbar/showMessage') {
					this.message = state.snackbar.message
					this.color = state.snackbar.color
					this.show = true
				}
			})
		},
		computed: {
			top: function () {
				return !this.$vuetify.breakpoint.mobile
			},
		},
	}
</script>

<style>
</style>
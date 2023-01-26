<script>
export default {
	data: function () {
		return {
			some_data: [],
		}
	},
	methods: {
		async refresh() {
			try {
				let response = await this.$axios.get("/links")
				this.some_data = response.data
			} catch (e) {
				alert(e.toString())
			}
		},

		async ldelete(id) {
			try {
				let response = await this.$axios.delete("/links/" + id)
				this.refresh()
			} catch (e) {
				alert(e.toString())
			}
		},
	},
	mounted() {
		this.refresh();

		console.log(this.$vuetify)

		this.$grammy.MainButton.setParams({
			text: "pulsantone inutile",
			color: this.$grammy.themeParams.hint_color,
			is_active: false,
			is_visible: false,
		});
	}
}
</script>

<template>
	<div class="layout">
		<v-table>
			<thead>
				<tr>
					<th class="text-left">
						X
					</th>
					<th class="text-left">
						Type
					</th>
					<th class="text-left">
						Description
					</th>
					<th class="text-left">
						Link
					</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="item in some_data" :key="item.id">
					<td><v-icon @click="ldelete(item.id)" icon="mdi-delete-outline" style="color: #E53935"></v-icon></td>
					<td>{{ item.type }}</td>
					<td>{{ item.description }}</td>
					<td><a style="text-decoration:none" :href="item.link" target="_blank"><v-icon icon="mdi-open-in-new"></v-icon></a>
					</td>
				</tr>
			</tbody>
		</v-table>
	</div>
</template>

<style>

</style>

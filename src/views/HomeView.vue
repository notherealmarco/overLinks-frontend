<script>
export default {
	data: function () {
		return {
			errormsg: null,
			loading: false,
			some_data: [],
		}
	},
	methods: {
		async refresh() {
			this.loading = true;
			this.errormsg = null;
			try {
				let response = await this.$axios.get("/links");
				this.some_data = response.data;
			} catch (e) {
				this.errormsg = e.toString();
			}
			this.loading = false;
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
					<td>{{ item.type }}</td>
					<td>{{ item.description }}</td>
					<td><a style="text-decoration:none" :href="item.link"><v-icon icon="mdi-open-in-new"></v-icon></a>
					</td>
				</tr>
			</tbody>
		</v-table>
	</div>
</template>

<style>

</style>

<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>
<script>
export default {}
</script>

<template>

	<v-app>
		<v-container class="fill-height">
			<v-row align-content="center" justify="center" class="fill-height">



				<router-view></router-view>


			</v-row>
		</v-container>
	</v-app>




</template>

<style>

</style>
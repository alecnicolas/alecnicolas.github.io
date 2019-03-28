<template>
	<div id="app">
		<div class="container">
            <h1>Highlighter</h1>
			<highlighter></highlighter>
		</div>
	</div>
</template>

<script>
import Highlighter from "./components/Highlighter.vue";
export default {
	name: "app",
	components: {
		Highlighter
	}
};
</script>

<style>
#app {
	font-family: "Avenir", Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>

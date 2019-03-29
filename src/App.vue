<template>
	<div id="app">
		<div class="container mt-5">
			<div class="text-center">
				<h1 style="color: cornflowerblue">Highlighter 🚀</h1>
			</div>
			<highlight-rules @add-rule="appendRule" @clear-rules="clearRules"/>
			<highlight-display :highlights="this.highlights"/>
			<highlighter :highlights="this.highlights" class="my-3"/>
			<h3>Output Text</h3>
			<div id="output" class="py-3" style="font-size: 1.25rem; overflow-wrap: break-word;">Example Text</div>
		</div>
	</div>
</template>

<script>
import Highlighter from "./components/Highlighter.vue";
import HighlightRules from "./components/HighlightRules.vue";
import HighlightDisplay from "./components/HighlightDisplay.vue";
export default {
	name: "app",
	data() {
		return {
			highlights: []
		};
	},
	components: {
		Highlighter,
		HighlightRules,
		HighlightDisplay
	},
	methods: {
		appendRule(event) {
			this.highlights.push({
				startOffset: event.start,
				endOffset: event.end,
				color: event.color,
				priority: event.priority
			});
		},
		clearRules() {
			this.highlights = [];
		}
	}
};
</script>

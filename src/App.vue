<template>
	<div id="app">
		<div class="container mt-5">
			<div class="text-center">
				<h1 class="header__text">Highlight.me 🚀</h1>
			</div>
			<div class="card">
				<highlight-rules @add-rule="appendRule" @clear-rules="clearRules"/>
				<highlight-display :highlights="this.highlights"/>
			</div>
			<div class="card">
				<highlighter class="my-3" :highlights="this.highlights"/>
				<h3>Output Text</h3>
				<div id="output" class="output__text py-3">Example Text</div>
			</div>
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

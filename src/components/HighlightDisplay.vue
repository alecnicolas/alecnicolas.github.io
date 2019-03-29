<template>
	<div>
		<button
			class="btn btn-secondary btn-sm"
			type="button"
			data-toggle="collapse"
			data-target="#highlightRules"
			aria-expanded="false"
			aria-controls="collapseExample"
		>{{highlights.length}} Applied Rules</button>
		<div class="collapse" id="highlightRules">
			<div class="card card-body">{{highlights}}</div>
		</div>
	</div>
</template>
<script>
export default {
	props: ["highlights"]
};
</script>

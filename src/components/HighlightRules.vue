<template>
	<div>
		<h3>Enter New Rules</h3>
        <div v-if="error" class="alert alert-danger alert-dismissible fade show" role="alert">
			<strong>Oops!</strong> Please fill out all of the forms!
			<button
				type="button"
				class="close"
                @click="error = false"
				aria-label="Close"
			>
				<span aria-hidden="true">&times;</span>
			</button>
		</div>
		<form class="row">
			<div class="form-group col-6 col-md-3">
				<label for="startOffset" title="Index where highlight begins">StartOffset</label>
				<input
					type="number"
					id="startOffset"
					class="form-control"
					placeholder="0"
					v-model="form.start"
					required
				>
			</div>
			<div class="form-group col-6 col-md-3">
				<label for="endOffset" title="Index where highlight ends">EndOffset</label>
				<input
					type="number"
					id="endOffset"
					class="form-control"
					placeholder="0"
					v-model="form.end"
					required
				>
			</div>
			<div class="form-group col-6 col-md-3">
				<label for="color" title="The color of your highlight">Hex Code (Color)</label>
				<div class="input-group">
					<div class="input-group-prepend">
						<span class="input-group-text" id="basic-addon1">#</span>
					</div>
					<input
						type="text"
						id="color"
						class="form-control"
						placeholder="000000"
						v-model="form.color"
						maxlength="6"
						required
					>
				</div>
			</div>
			<div class="form-group col-6 col-md-3">
				<label for="priority" title="Lower numbers have higher highlight priority">Priority</label>
				<input
					type="number"
					id="priority"
					class="form-control"
					placeholder="0"
					v-model="form.priority"
					required
				>
			</div>
			<div class="col-12 text-center">
				<button type="button" class="btn btn-danger btn-sm mx-1" @click.prevent="clearRules">Clear</button>
				<button type="submit" class="btn btn-primary btn-sm mx-1" @click.prevent="addRule">Add Rule</button>
			</div>
		</form>
	</div>
</template>
<script>
export default {
	data() {
		return {
			form: {
				start: null,
				end: null,
				color: null,
				priority: null
            },
            error: false
		};
	},
	methods: {
		addRule() {
            if (this.checkForm()){
                this.$emit("add-rule", this.form)
                for(let k in this.form){
                    this.form[k] = null
                }
            }
            else
                this.error = true
		},
		clearRules() {
			this.$emit("clear-rules");
		},
		checkForm() {
			for (let key in this.form) {
				if (this.form[key] == null) return false;
			}
			return true;
		}
	}
};
</script>

<template>
	<div class="my-3">
		<h3>Text to Highlight</h3>
		<div class="row">
			<div class="col-12 text-center">
				<div class="form-group">
					<textarea type="text" class="form-control" v-model="inputString" @keyup.enter="highlightText" placeholder="Write a sentence or two"/>
				</div>
				<button type="button" class="btn btn-primary btn-block" @click.prevent="highlightText">Apply Highlighting</button>
			</div>
		</div>
	</div>
</template>
<script>
export default {
	props: ["highlights"],
	data() {
		return {
			inputString: "",
			outputString: ""
		};
	},
	methods: {
		//Main text highlight function
		highlightText() {
			this.sortByPriority();
			let result = "";

			let priorityArray = this.populatePriorityArray();
			let offsetArray = this.countOffset(priorityArray);

			let count = 0;
			for (let i = 0; i < offsetArray.length; i++) {
				if (offsetArray[i].color != null) {
					result +=
						'<span style="background-color: #' +
						offsetArray[i].color +
						'; border-radius: 3px;" >' +
						this.inputString.substr(count, offsetArray[i].span) +
						"</span>";
					count += offsetArray[i].span;
				} else {
					result +=
						"<span>" +
						this.inputString.substr(count, offsetArray[i].span) +
						"</span>";
					count += offsetArray[i].span;
				}
			}

			result += "<span>" + this.inputString.substr(count) + "</span>";
			this.inputString = "";
			document.querySelector("#output").innerHTML = result;
		},

		sortByPriority() {
			this.highlights.sort(function(first, second) {
				return second.priority - first.priority;
			});
		},

		populatePriorityArray() {
			let placement = [];
			for (let i = 0; i < this.highlights.length; i++) {
				let highlight = this.highlights[i];
				let start = Number(highlight.startOffset);
                let end = Number(highlight.endOffset);
                
				for (let j = start; j < end; j++) {
					placement[j] = i;
				}
			}
			return placement;
		},

		countOffset(placement) {
			let curr = placement[0];
			let offsetSize = [];
			if (curr != null)
				offsetSize = [
					{
						color: this.highlights[curr].color,
						span: 1
					}
				];
			else offsetSize = [{ color: null, span: 1 }];

			let index = 0;
			for (let i = 1; i < placement.length; i++) {
				if (curr != placement[i]) {
					curr = placement[i];
					index += 1;
					if (curr != null)
						offsetSize[index] = {
							color: this.highlights[curr].color,
							span: 1
						};
					else offsetSize[index] = { color: null, span: 1 };
				} else offsetSize[index].span += 1;
			}
			return offsetSize;
		}
	}
};
</script>

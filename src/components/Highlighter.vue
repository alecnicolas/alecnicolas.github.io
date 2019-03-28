<template>
	<div>
		<div class="col-10">
			<div id="output" class="py-3"></div>
			<div class="input-group">
				<input type="text" class="form-control" v-model="inputString" placeholder="Enter a string">
				<button type="button" class="btn btn-primary" @click.prevent="highlightText">Highlight!</button>
			</div>
		</div>
	</div>
</template>
<script>
export default {
	data() {
		return {
			//You will deliver new technology with an adorable puppy. Perfect!
			inputString: "",
			outputString: "",
			highlights: [
				{
					startOffset: 2,
					endOffset: 36,
					color: "skyblue",
					priority: 3
				},
				{
					startOffset: 0,
					endOffset: 40,
					color: "lightpink",
					priority: 8
				},
				{
					startOffset: 24,
					endOffset: 34,
					color: "yellow",
					priority: 2
				},
				{
					startOffset: 50,
					endOffset: 60,
					color: "#d9f593",
					priority: 0
				}
			]
		};
	},
	methods: {
		highlightText() {
			this.sortByPriority();
			let result = "";

			let priorityArray = this.populatePriorityArray();
			let offsetArray = this.countOffset(priorityArray);

			let count = 0;
			for (let i = 0; i < offsetArray.length; i++) {
				if (offsetArray[i].color != null) {
					result +=
						'<span style="background-color:' +
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
				for (
					let j = highlight.startOffset;
					j < highlight.endOffset;
					j++
				) {
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

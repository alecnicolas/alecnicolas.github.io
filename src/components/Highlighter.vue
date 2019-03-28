<template>
	<div class="row justify-content-center">
		<div class="col-8">
			<div class="input-group">
				<input type="text" class="form-control" :model="inputString">
				<button type="button" class="btn btn-primary" @click.prevent="highlightText">Highlight!</button>
			</div>
		</div>
	</div>
</template>
<script>
export default {
	data() {
		return {
			inputString: "abcdefgh",
			highlights: [
                {
                    startOffset: 1,
                    endOffset: 4,
                    color: 'blue',
                    priority: 3
                },
                {
                    startOffset: 0,
                    endOffset: 2,
                    color: 'red',
                    priority: 8
                },
                {
                    startOffset: 3,
                    endOffset: 6,
                    color: 'yellow',
                    priority: 0
                }
            ]
		};
	},
	methods: {
        highlightText() {
            this.sortPriority()
            let result = ""

            for (let i=0; i<this.highlights.length; i++){
                let highlight = this.highlights[i]
                result += this.inputString.substring(highlight.startOffset, highlight.endOffset)
            }

            console.log(result)
        },

        sortPriority() {
            this.highlights.sort(function(first, second){
                return first.priority - second.priority
            })
        }
    }
};
</script>

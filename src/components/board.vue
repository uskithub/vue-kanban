<template lang="pug">
	ul.kanban-board-container
		li.kanban-board(v-for="board in boards", :key="board.id")
			span.kanban-board-header
				legend {{ board.name }}
			div.drag-options
			ul.kanban-list(data-type="board"
				@dragenter="ondragenter($event, board)"
				@dragleave="ondragleave($event, board)"
			)
				kanban(v-for="kanban in board.kanbans", :kanban="kanban", :key="kanban.id")
</template>
<script>
	export default {
		name: "Board"
        , props: {
			boards : {
				type: Array
				, validator: (value) => { return true; } // TODO
			}
		}
		, computed: {
		}
		, data() {
			return {
				draggingOver : null
			}
		}
		, methods : {
			ondragenter(e, board) {
				const elem = e.target
					, type = elem.dataset.type
					, id = elem.dataset.id
					;

				if (type !== undefined) {
					elem.classList.add("drop-target");
					this.draggingOver = elem;
				}

				if (type === "kanban") {
					console.log(`[enter]@${board.name}:${id}: ${elem.dataset.type}`, e);
				} else {
					console.log(`[enter]@${board.name}: ${elem.dataset.type}`, e);
				}
			}
			, ondragleave(e, board) {
				const elem = e.target
					, type = elem.dataset.type
					;
				elem.classList.remove("drop-target");
				if (this.draggingOver == elem) {
					this.draggingOver = null;
				}
				
				console.log(`[leave]@${board.name}`);
			}
		}
	};
</script>

<style lang="scss">
    @import "../assets/style";
</style>
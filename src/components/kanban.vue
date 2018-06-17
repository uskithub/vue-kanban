<template lang="pug">
	li.kanban-item(draggable="true", :key="kanban.id" 
		@click="$emit('click', $event, kanban)"
		@dragstart="ondragstart($event, kanban)"
		@dragend="ondragend($event, kanban)"
	)
		slot(:name="kanban.name")
			.media-content
				strong  {{ kanban.name }}
				ul.kanban-list(v-if="kanban.kanbans !== undefined && kanban.kanbans.length > 0" data-type="kanban", :data-id="kanban.id")
					kanban(v-for="child in kanban.kanbans", :kanban="child", :key="child.id")
</template>

<script>
	import { cloneDeep, isObject } from "lodash";
	
	// Summary:
	//  - kanban corresponds to a task.
	//	- kanbans may contain an other kanban-list.
	
	// Interface:
	//  - kanban emits click events with the task.

	export default {
		name: "Kanban"
        , props: {
			kanban: {
				type: Object
				, validator: (value) => { return true; } // TODO
			}
			, isDisplayShortname: {
				type: Boolean
				, default: false
			}
			, isDraggable : {
				type: Boolean
				, default: true
			}
		}
		, data() {
			return {
				dragging : null
			}
		}
		, computed: {
        }
        , methods: {
            ondragstart(e, kanban) {
				this.dragging = e.target;
                console.log("[start]", kanban);
			}
			, ondragend(e, kanban) {
				this.dragging = null;
                console.log("[end]", kanban);
			}
        }
	};
</script>

<style lang="scss">
	@import "../assets/style";
</style>
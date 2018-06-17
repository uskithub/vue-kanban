<template lang="pug">
	board(:boards="boards" @arrange="onarrange")
</template>

<script>
	export default {
		name: 'HelloWorld'
		, data () {
			return {
				boards: [
					{
						id: "a"
						, name: "board1"
						, kanbans: [
							{
								id: "a01"
								, name: "a-kanban01"
								, kanbans: [
									{
										id: "a-child01"
										, name: "a-child-kanban01"
									}
								]
							}
							, {
								id: "a02"
								, name: "a-kanban02"
							}
						]
					}
					, {
						id: "b"
						, name: "board2"
						, kanbans: [
							{
								id: "b01"
								, name: "b-kanban01"
								, kanbans: [
									{
										id: "b-child01"
										, name: "b-child-kanban01"
									}
								]
							}
							, {
								id: "b02"
								, name: "b-kanban02"
							}
						]
					}
				]
			}
		}
		, methods : {
			onarrange({ kanban, from, to, index }) {
				console.log(kanban, from, to, index);
			}
		}
	}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	h1, h2 {
		font-weight: normal;
	}
	ul {
		list-style-type: none;
		padding: 0;
	}
	li {
		display: inline-block;
		margin: 0 10px;
	}
	a {
		color: #42b983;
	}
</style>

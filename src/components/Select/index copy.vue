<template>
	<div class="hello">
		<label for="pet-select">Choose a pet:</label>
		<select name="pets" id="pet-select" @change="handleSelect">
			<option value="">{{ placeholder }}</option>
			<option v-for="opt in options" :key="opt.label">
				{{ opt.label }}
			</option>
		</select>
	</div>
</template>

<script>
export default {
	name: 'Select',
	props: {
		placeholder: {
			type: String,
			default: () => '--Please choose an option--',
		},
		options: Array,
		value: String,
	},
	mounted() {
		console.log(this.value);
	},
	methods: {
		handleSelect(val) {
			this.value = val.target.value;
			// console.log(val.target.value);
			this.$emit('select', val.target.value);
		},
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
	margin: 40px 0 0;
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

<template>
	<div id="app">
		<img alt="Vue logo" src="./assets/logo.png" />
		<Select
			v-model="value"
			:placeholder="placeholder"
			:options="options"
      multiple
		></Select>
	</div>
</template>

<script>
import Select from './components/Select';

export default {
	name: 'App',
	components: {
		Select,
	},
	data() {
		return {
			options: [
				{ id: 'dog', value: 'dog', label: '狗' },
				{ id: 'cat', value: 'cat', label: '猫' },
				{ id: 'hamster', value: 'hamster', label: '仓鼠' },
				{ id: 'parrot', value: 'parrot', label: '鹦鹉' },
				{ id: 'spider', value: 'spider', label: '蜘蛛' },
				{ id: 'goldfish', value: 'goldfish', label: '金鱼' },
			],
			placeholder: '---请选择---',
			value: '',
		};
	},
	methods: {
		onSelect(val) {
			console.log('parent onSelect', val);
		},
	},
	watch: {
		value(newVal, oldVal) {
			console.log(newVal, oldVal);
		},
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>

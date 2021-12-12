<template>
	<div class="select-wrapper">
		<div class="select-input" :class="{ 'select-open': isShow }">
			<input
				name="pets"
				type="text"
				:value="getValue"
				id="pet-select"
				readonly="readonly"
				:placeholder="placeholder"
				@click.stop="handleClick"
			/>
			<div class="dropdown-btn" @click.stop="handleClick"></div>
		</div>

		<div class="options-wrapper" :class="{ 'options-open': isShow }">
			<ul class="options">
				<li
					class="option"
					v-for="item in options"
					:key="item.id"
					@click="handlValue(item)"
					:class="{ selected: isSelected(item) }"
				>
					{{ item.label }}
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Select',
	data() {
		return {
			singleValue: '',
			multipleValue: [],
			isShow: false,
		};
	},
	model: {
		prop: 'value',
		event: 'aaa',
	},
	props: {
		placeholder: {
			type: String,
			default: () => '--Please choose an option--',
		},
		multiple: {
			type: Boolean,
			default: false,
		},
		options: Array,
		value: [String, Object, Array],
	},
	mounted() {
		// 点击下拉内容以外的隐藏下拉内容
		document.addEventListener('click', (e) => {
			let className = [
				'options-wrapper',
				'options',
				'option',
				'option selected',
			];
			if (!className.includes(e.target.className)) {
				console.log(e.target.className);
				this.isShow = false;
			}
		});
	},
	methods: {
		handleClick() {
			this.isShow = true;
		},
		handlValue(val) {
			if (!this.multiple) {
				// 单选
				this.singleValue = val;
				this.isShow = false;
				this.$emit('aaa', this.singleValue.value);
			} else {
				// 多选
				const index = this.multipleValue.indexOf(val);
				if (index > -1) {
					this.multipleValue.splice(index, 1);
				} else {
					this.multipleValue.push(val);
				}
				this.$emit('aaa', this.getMultiLabel());
			}
		},
		isSelected(item) {
			if (this.multiple && this.multipleValue.includes(item)) {
				return true;
			}
			if (!this.multiple && this.singleValue === item) {
				return true;
			}
		},
		getMultiLabel() {
			return this.multipleValue.map((item) => item.label);
		},
	},
	computed: {
		getValue() {
			if (this.multiple) {
				return this.getMultiLabel().join(',');
			}
			return this.singleValue.label || '';
		},
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
	box-sizing: border-box;
}
h3 {
	margin: 40px 0 0;
}
ul {
	margin: 0;
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

.select-wrapper {
	margin: 0 auto;
	width: 180px;
	height: 100px;
}

.select-wrapper .select-input {
	display: flex;
	border: 1px solid #ccc;
	border-radius: 4px;
	transition: border 0.15s ease-in-out;
}

.select-wrapper .select-input.select-open {
	border-color: #42b983;
}

.select-wrapper .select-input input {
	width: 100%;
	height: 30px;
	padding: 0 8px;
	cursor: default;
	user-select: none;
	border: none;
	border-radius: 4px;
}

.select-wrapper .select-input input:focus-visible {
	outline: none;
}

.dropdown-btn {
	position: relative;
	flex: 0 0 30px;
	height: 30px;
	background-color: #fff;
	border-radius: 4px;
}

.dropdown-btn::before {
	content: '';
	position: absolute;
	top: 5px;
	display: block;
	width: 1px;
	height: 20px;
	border-radius: 4px;
	background-color: #42b983;
}

.dropdown-btn::after {
	content: '';
	position: absolute;
	top: calc(50% - 2px);
	left: calc(50% - 4px);
	display: block;
	border: 4px solid transparent;
	border-top: 4px solid #42b983;
	width: 0px;
}

.options-wrapper {
	display: none;
	margin-top: -1px;
	width: 100%;
	border: 1px solid #42b983;
	box-shadow: 0 2px 20px 0 #42b98380;
	border-radius: 4px;
}
.options {
	display: flex;
	flex-direction: column;
	width: 100%;
}
.option {
	position: relative;
	margin: 0;
	padding: 4px 10px;
	width: 100%;
	cursor: pointer;
	font-size: 14px;
	text-align: left;
}
.option.selected {
	color: #fff;
	background-color: #42b983;
}
.option.selected::after {
	content: '√';
	position: absolute;
	display: block;
	right: 10px;
	top: 8px;
}
.option:hover {
	background-color: #42b983;
}
.options-open {
	display: block;
}
</style>

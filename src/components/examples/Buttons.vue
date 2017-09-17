<template>
	<div>
		<div class="generator">
			<div class="config">
				<div><label>id<input v-model="elementProperties.id" /></label></div>
				<div><label>link<input v-model="elementProperties.link" /></label></div>
				<div><label>iconClass<input v-model="elementProperties.iconClass" /></label></div>
				<div><label>content<input v-model="elementProperties.content" /></label></div>
				<div><label>submit<input type="checkbox" v-model="elementProperties.submit" /></label></div>

				<div><label>type<select v-model="elementProperties.type">
					<option v-for="type in config.type" v-bind:value="type">{{ type }}</option>
				</select></label></div>

				<div>
					<label>theme
						<select v-model="elementProperties.theme">
							<option v-for="theme in config.theme" v-bind:value="theme">{{ theme }}</option>
						</select>
					</label>
				</div>
			</div>

			<div class="result">
				<div class="visual">
					<div v-html="buttonElement"></div>
				</div>
				<div class="markup">
					<span>import * as quark from 'quark-gui';</span>
					<span>let Button = quark.Atoms.Buttons.Button;</span>
					<span>Button.getModule(</span>
					<pre v-html="elementProperties"></pre>
					<span>);</span>
				</div>
			</div>
		</div>
	</div>
</template>


<script>
import * as quark from "quark-gui";

let Button = quark.Atoms.Buttons.Button;

export default {
	name: 'Buttons',
	data: function () {
		return {
			elementProperties: {
				id: '',
				link: '',
				iconClass: '',
				content: '',
				title: '',
				type: 'flat',
				theme: 'default',
				submit: false
			},
			config: {
				theme: ['default', 'primary', 'info', 'success', 'warning', 'danger'],
				type: ['flat', 'raised', 'minimal']
			}

		}
	},
	computed: {
		buttonElement: function (){
			return Button.getModule(this.elementProperties)
		},
		buttonElementMarkup: function (){
			return this.elementProperties;
		}
	}
}
</script>

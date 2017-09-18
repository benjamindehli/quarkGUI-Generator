<template>
	<div>
		<div class="generator">
			<h2>Button</h2>
			<div class="row">
				<div class="config col-sm-4">
					<h3>Properties</h3>
					<div><label>ID<input v-model="elementProperties.id" /></label></div>
					<div><label>Link<input v-model="elementProperties.link" /></label></div>
					<div><label>Icon class<input v-model="elementProperties.iconClass" /></label></div>
					<div><label>Content<input v-model="elementProperties.content" /></label></div>
					<div><label>Submit<input type="checkbox" v-model="elementProperties.submit" /></label></div>

					<div><label>Type<select v-model="elementProperties.type">
						<option v-for="type in config.type" v-bind:value="type">{{ type }}</option>
					</select></label></div>

					<div>
						<label>Theme
							<select v-model="elementProperties.theme">
								<option v-for="theme in config.theme" v-bind:value="theme">{{ theme }}</option>
							</select>
						</label>
					</div>
				</div>

				<div class="result col-sm-8">
					<h3>Result</h3>
					<div class="tabs">
						<span class='tab tab-preview' v-bind:class="{active: resultOptions.show == 'preview'}" v-on:click="resultOptions.show = 'preview'">Preview</span>
						<span class='tab tab-markup' v-bind:class="{active: resultOptions.show == 'markup'}" v-on:click="resultOptions.show = 'markup'">Markup</span>
					</div>
					<div v-show="resultOptions.show == 'preview'" class="preview">
						<div v-html="buttonElement"></div>
					</div>
					<div v-show="resultOptions.show == 'markup'" class="markup">
						<span>import * as quark from 'quark-gui';</span>
						<span>let Button = quark.Atoms.Buttons.Button;</span>
						<span>Button.getModule(</span>
						<pre v-html="elementProperties"></pre>
						<span>);</span>
					</div>
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
				content: 'button',
				title: '',
				type: 'flat',
				theme: 'default',
				submit: false
			},
			config: {
				theme: ['default', 'primary', 'info', 'success', 'warning', 'danger'],
				type: ['flat', 'raised', 'minimal']
			},
			resultOptions:{
				show: 'preview'
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

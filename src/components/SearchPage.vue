<template>
  <div class="container-fluid">
    <div class="search-wrapper">
			<!-- check boxes -->
			<div id="checkboxes">
				<div v-for="(stack,index) in stacks" :key="index" class="form-check form-check-inline">
					<input class="form-check-input" type="checkbox"  v-model="stack.checked" @change="getfilteredData">
					<label class="form-check-label">
						{{ stack.value }}
					</label>
				</div>
			</div>
		</div>
		<!-- end of checkboxes -->
    <div class="card-columns">
			<!-- iterate data -->
      <item-card v-for="(item, index) in filteredData" :key="index" :item="item"></item-card>
    </div>
  </div>
</template>

<script>
import ItemCard from './ItemCard';
import data from '../data/data';

export default {
	name: 'SearchPage',
	components: {
		'item-card': ItemCard
	},
	computed: {
		selectedFilters: function() {
			let filters = [];
			let checkedFiters = this.stacks.filter(obj => obj.checked);
			checkedFiters.forEach(element => {
				filters.push(element.value);
			});
			return filters;
		}
	},
	data() {
		return {
			filteredData: [],
			search: '',
			stacks: [
				{
					checked: false,
					value: 'language'
				},
				{
					checked: false,
					value: 'framework'
				},
				{
					checked: false,
					value: 'frontend'
				},
				{
					checked: false,
					value: 'backend'
				},
				{
					checked: false,
					value: 'mobile'
				},
				{
					checked: false,
					value: 'web'
				},
				{
					checked: false,
					value: 'hybrid'
				},
				{
					checked: false,
					value: 'database'
				}
			]
		};
	},
	methods: {
		getfilteredData: function() {
			this.filteredData = data;
			let filteredDataByfilters = [];
			// first check if filters where selected
			if (this.selectedFilters.length > 0) {
				filteredDataByfilters= this.filteredData.filter(obj => this.selectedFilters.every(val => obj.stack.indexOf(val) >= 0));
				this.filteredData = filteredDataByfilters;
			} 
		}
	},
	mounted() {
		this.getfilteredData();
	}
};
</script>

<template>
  <div class="card p-3">
    <div class="text-center">
      <img class="img-fluid" :src="item.logo" width="100" alt="Card image cap">
      <div class="card-body">
        <h5 class="card-title">{{ item.name }} </h5>
      </div>
    </div>
  </div>
</template>

<script>
export default {
	data() {
		return {};
	},
	props: {
		item: {
			type: Object,
			required: true
		}
	}
};
</script>


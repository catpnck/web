<script>
export default {
    props: {
	id:     Number,
	name:   String,
	surn:   String,
},
emits: ['remove'],
}
</script>

<template>
	{{ name }}
	{{ surn }}
	
	<button @click="$emit('remove', id)">
		remove
	</button>
</template>
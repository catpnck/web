<script>
import User from './components/User.vue'

export default {
  components: {
    User
  },
  data() {
    return {
      users: [
        {
          id: 1,
          name: 'name1',
          surn: 'surn1'
        },
        {
          id: 2,
          name: 'name2',
          surn: 'surn2'
        },
        {
          id: 3,
          name: 'name3',
          surn: 'surn3'
        },
      ],
    }
  },
  methods: {
    remove(id) {
      this.users = this.users.filter((user) => {
        return user.id !== id;
      })
    }
  }
}
</script>

<template>
	<User
		v-for   ="user in users"
		
		:id     ="user.id"
		:name   ="user.name"
		:surn   ="user.surn"
		@remove ="remove"
		:key    ="user.id"
	/>
</template>

<style scoped></style>

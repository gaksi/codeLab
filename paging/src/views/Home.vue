<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <newer/>
  </div>
</template>

<script>
// @ is an alias to /src
import pagingList from '@/components/paging-list.vue'
import newer from '@/components/newer.vue'

export default {
  name: 'home',
  components: {
    pagingList, newer
  }
}
</script>

<template>
    <p><!-- 한 번에 보여줄 리스트 갯수[10, 20, 50], 한 번에 보여줄 페이징 버튼 수[5, 10]-->
        <label for="item-size">Show items:</label>
        <select v-model.number="itemSize" id="item-size"
                @change="handler('item')">
            <option v-for="(value, index) in itemSizeOptions" :key="index">
                {{ value }}
            </option>
        </select>
        <label for="page-size">Show pages:</label>
        <select v-model.number="pageSize" id="page-size"
                @change="handler('page')">
            <option v-for="(value, index) in pageSizeOptions" :key="index">
                {{ value }}
            </option>
        </select>
    </p>
</template>

<script>
    export default {
        name: "show-select.vue",
        props: ['itemSizeOptions', 'pageSizeOptions'],
        data() {
          return {
              itemSize: 10,
              pageSize: 5
          }
        },
        methods: {
            resetPage() {
                this.$emit('pageReset')
            },
            changeItemSize(size) {
                this.$emit('changeItemSize', size)
            },
            changePageSize(size) {
                console.log('change page!')
                this.$emit('changePageSize', size)
            },
            handler(plague) {
                this.resetPage();
                if(plague === 'item') this.changeItemSize(this.itemSize);
                else this.changePageSize(this.pageSize);
            }
        }
    }
</script>

<style scoped>

</style>

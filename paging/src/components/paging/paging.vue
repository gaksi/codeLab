<template>
    <!-- 페이징 버튼 -->
    <div>
        <div class="paging"  v-if="total > 0">
            <button type="button"
                    :disabled="!pagingData.prevPage"
                    @click="onPageClick(pagingData.prevPage)">Prev</button>

            <button v-for="newPage in pagingData.pages" :key="newPage"
                    :class="{ active: page === newPage }"
                    @click="onPageClick(newPage)">{{ newPage }}</button>

            <button type="button"
                    :disabled="!pagingData.nextPage"
                    @click="onPageClick(pagingData.nextPage)">Next</button>
        </div>
        <!--총 리스트 갯수-->
        <p>Total: {{ total }}</p>
    </div>

</template>

<script>
    export default {
        name: "paging.vue",
        props: ['pagingData', 'total', 'page'],
        created() {
            console.log(this.pagingData)
        },
        methods: {
            onPageClick(pageMove) {
                this.$emit('pageClick', pageMove)
            }
        }
    }
</script>

<style scoped>

</style>

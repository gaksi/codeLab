<template>
    <div>
        <show-select :itemSizeOptions="[10, 20, 50]" :pageSizeOptions="[5, 10]"
        @changeItemSize="changeItemSize" changePageSize="changePageSize"></show-select>
        <list-table :items="items"></list-table>
        <paging :pagingData="pagingData" :total="total"
        @pageClick="onPageClick"></paging>

    </div>
</template>

<script>
    import showSelect from '@/components/paging/show-select.vue'
    import paging from '@/components/paging/paging.vue'
    import listTable from '@/components/paging/list-table.vue'
    /*
     * TO-DO: Array.slice, Math.floor, Math.ceil, Math.min, Math.max 사용법 확인
     */
    function getRandomNumber(min, max) {
        const count = max - min + 1;
        return Math.floor(Math.random() * count) + min
    }
    export default {
        name: "paging-list.vue",
        data() {
            return {
                allItems: [],
                page: 1, // 현재 페이지
                itemSize: 10, // 한 페이지에 노출할 item 수
                pageSize: 5 // 한번에 노출할 페이징 수
            }
        },
        component: {
            showSelect, paging, listTable
        },
        computed: {
            items () {
                const start = (this.page - 1) * this.itemSize;
                const end = Math.min(start + this.itemSize, this.allItems.length);
                return this.allItems.slice(start, end)
            },
            total () {
                return this.allItems.length
            },
            pagingData () {
                // 전체 페이지 수
                const pageCount = Math.ceil(this.total / this.itemSize);
                // 페이지 블록(ex: [1, 2, 3, 4, 5]) 수
                const blockCount = Math.ceil(pageCount / this.pageSize);
                // 현재 페이지 블록이 몇 번째인지
                const currentBlock = Math.ceil(this.page / this.pageSize);
                // 페이지 블록 첫 페이지
                const pageStart = (currentBlock - 1) * this.pageSize + 1;
                // 페이지 블록 마지막 페이지
                const pageEnd = Math.min(pageStart + this.pageSize - 1, pageCount);
                const pages = [];

                for (let i = pageStart; i <= pageEnd; i++) {
                    pages.push(i)
                }

                let prevPage = null;
                let nextPage = null;

                if (currentBlock > 1) {
                    prevPage = pages[0] - 1
                }

                if (currentBlock < blockCount) {
                    nextPage = pages[pages.length - 1] + 1
                }

                const pagingData = {
                    pages,
                    prevPage,
                    nextPage
                };

                console.log(pagingData);
                return pagingData
            }
        },
        created () {
            const count = getRandomNumber(100, 200);

            for (let i = 1; i <= count; i++) {
                this.allItems.push({
                    id: i,
                    title: `item-${i}`,
                    date: new Date().toLocaleString('ko-KR')
                })
            }
            console.log(`${count} items are created`)
        },
        methods: {
            resetPage () {
                this.page = 1
            },
            onPageClick (page) {
                this.page = page
            },
            changeItemSize(val) {
                this.itemSize = val
            },
            changePageSize(val) {
                this.pageSize = val
            }
        }
    }
</script>

<style scoped>
    body { font-size: 13px; font-family: sans-serif; }
    .data-table { border-collapse: collapse; font-size: inherit; }
    .data-table th,
    .data-table td {padding: 2px 4px; border: 1px solid #eee; }
    .active { font-weight: bold; text-decoration: underline; }
</style>

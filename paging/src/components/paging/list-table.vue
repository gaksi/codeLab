<template>
    <!-- 리스트 뿌리기 -->
    <table class="data-table">
        <tr>
            <th>id</th>
            <th>title</th>
            <th>date</th>
        </tr>
        <tr v-for="item in items" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.title }}</td>
            <td>{{ item.date }}</td>
        </tr>
    </table>
</template>

<script>
    export default {
        name: "list-table.vue",
        props: ['items']
    }
</script>

<style scoped>

</style>

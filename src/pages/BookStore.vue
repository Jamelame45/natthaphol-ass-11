<template>
    <Navbar />
    <section class="about">
        <h1 class="heading"> book <span>store</span> </h1>
        <a-table :columns="columns" :data-source="data" :rowKey="(record) => record.id">
            <template #action="{ record }">
                <a href="javascript:void(0)" @click="showModal(record.id)">แก้ไข</a>
                <a-divider type="vertical" />
                <a href="javascript:void(0)" @click="delete(record.id)">ลบ</a>
            </template>

        </a-table>
        <a-button type="primary" @click="showModal">เพิ่มหนังสือ</a-button>

    </section>

    <!-- Modal Here-->


</template>

<script>
import Navbar from "../components/Navbar.vue";
import axios from 'axios'
import { Modal } from 'ant-design-vue';
const columns = [
    {
        title: "id",
        dataIndex: "id",
        key: "id",
        width: 65,
    },
    {
        title: "ชื่อหนังสือ",
        dataIndex: "name",
        key: "name",
    },
    {
        title: "ราคา",
        dataIndex: "name",
        key: "price",
        align: 'right'
    },
    {
        title: "Action",
        slote: { customRender: "action" },
        key: "id",
        alighn: 'center',
        width: 150,
    }

];
export default {
    components: { Navbar },
    methods: {
        async getBooks() {
            try {
                let res= await axios.get("http://localhost:3000/books")
                this.data = res.data
            } catch (error) { }
        }
    },
    data() {
        return {
            columns: columns,
            data: []
        }
    },
    beforeMount() {
        this.getBooks()
    }
}
</script>

<style>

</style>
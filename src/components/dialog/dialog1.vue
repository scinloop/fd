<template>
    <div>
        <el-input v-model="searchValue" size="mini" clearable placeholder="请输入编号或城市" style="width:300px"></el-input>
        <el-button type="primary" size="mini" @click="doFilter">搜索</el-button>
        <el-table :data="tableData" border>
            <el-table-column prop="number" label="编号" width="180" align="center"></el-table-column>
            <el-table-column prop="name" label="姓名" width="180" align="center"></el-table-column>
            <el-table-column prop="address" label="地址" width="180" align="center"></el-table-column>
        </el-table>
        <el-pagination @size-change="handleSizeChange" @current-change="handleCurrentChange" :current-page="currentPage"
            :page-sizes="[1, 4, 8]" :page-size="pageSize" layout="total, sizes, prev, pager, next, jumper"
            :total="totalItems"></el-pagination>
    </div>
</template>

<script>
export default {
    data() {
        return {
            resData: [
                { number: "WH20160501", name: "王一虎", address: "武汉" },
                { number: "WH20160502", name: "王二虎", address: "武汉" },
                { number: "SH20160502", name: "王三虎", address: "上海" },
                { number: "SH20160503", name: "王四虎", address: "上海" },
                { number: "NJ20160503", name: "王五虎", address: "南京" },
                { number: "NJ20160504", name: "王六虎", address: "南京" },
                { number: "GZ20160505", name: "王七虎", address: "广州" },
                { number: "SZ20160505", name: "王八虎", address: "深圳" },
            ],
            searchValue: "",
            tableData: [],
            currentPage: 1,
            pageSize: 8,
            totalItems: 0,
            filterTableData: [],
            flag: false,
        };
    },
    methods: {
        mockRequset() {
            this.totalItems = this.resData.length; // 注意： 这里mock数据是写在data里的，请求需考虑异步的情况
            if (this.totalItems > this.pageSize) {
                for (let index = 0; index < this.pageSize; index++) {
                    this.tableData.push(this.resData[index]);
                }
            } else {
                this.tableData = this.resData;
            }
        },
        // 前端搜索功能需要区分是否检索,因为对应的字段的索引不同
        doFilter() {
            this.tableData = [];
            this.filterTableData = [];
            this.resData.filter((item) => {
                if ('number' in item || 'address' in item) {
                    // 按编号或地区查询 注意：根据实际数据 灵活调整字母大小写
                    if (item.number.toUpperCase().indexOf(this.searchValue.toUpperCase()) > -1
                        || item.address.indexOf(this.searchValue) > -1) {
                        this.filterTableData.push(item);
                    }
                }
            })
            // 页面数据改变重新统计数据数量和当前页
            this.currentPage = 1;
            this.totalItems = this.filterTableData.length;
            // 渲染表格,根据值
            this.currentChangePage(this.filterTableData);
            // 页面初始化数据需要判断是否检索过
            this.flag = true;
        },
        // 每页显示条数改变触发
        handleSizeChange(val) {
            console.log(`每页 ${val} 条`);
            this.pageSize = val;
            this.handleCurrentChange(1);
        },
        // 当前页改变触发
        handleCurrentChange(val) {
            console.log(`当前页: ${val}`);
            this.currentPage = val;
            // 判断是否为搜索的数据,传入对应值
            if (!this.flag) {
                this.currentChangePage(this.resData);
            } else {
                this.currentChangePage(this.filterTableData);
            }
        },
        // 根据分页，确定当前显示的数据
        currentChangePage(list) {
            let fromNum = (this.currentPage - 1) * this.pageSize;
            let toNum = this.currentPage * this.pageSize;
            this.tableData = [];
            for (; fromNum < toNum; fromNum++) {
                if (list[fromNum]) {
                    this.tableData.push(list[fromNum]);
                }
            }
        },
    },
    beforeMount() {
        this.mockRequset()
    }
};
</script>
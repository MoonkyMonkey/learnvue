<template>
    <el-row class="demo-autocomplete">
        <el-col :span="12">
            <div class="sub-title">选择标签</div>
            <el-autocomplete
            class="inline-input"
            v-model="state1"
            :fetch-suggestions="querySearch"
            placeholder="选择标签"
            @select="handleSelect"
            ></el-autocomplete>
        </el-col>
        <el-col :span="12">
            <el-input
            type="textarea"
            :autosize="{ minRows: 2 }"
            placeholder="请输入内容"
            v-model="textarea2">
            </el-input>
        </el-col>
        <el-col>
            <el-button type="success">增加笔记</el-button>
              <el-table
                :data="tableData"
                style="width: 100%">
                <el-table-column
                    prop="date"
                    label="标签"
                    width="180">
                </el-table-column>
                <el-table-column
                    prop="name"
                    label="笔记"
                    width="500">
                </el-table-column>
                </el-table>
        </el-col>
    </el-row>
</template>
<script>
export default {
  name: 'Select',
  data () {
    return {
      restaurants: [],
      state1: '',
      textarea2: '',
      tableData: [{
        date: 'Linux',
        name: '关于linux的笔记',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: 'Cplusplus',
        name: '关于c++的笔记',
        address: '上海市普陀区金沙江路 1517 弄'
      }, {
        date: 'vim',
        name: '关于vim的笔记',
        address: '上海市普陀区金沙江路 1519 弄'
      }]
    }
  },
  methods: {
    querySearch (queryString, cb) {
      var restaurants = this.restaurants
      var results = queryString ? restaurants.filter(this.createFilter(queryString)) : restaurants
      // 调用 callback 返回建议列表的数据
      cb(results)
    },
    createFilter (queryString) {
      return (restaurant) => {
        return (restaurant.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0)
      }
    },
    loadAll () {
      return [
        { 'value': 'Linux', 'address': '长宁区新渔路144号' },
        { 'value': 'Cplusplus', 'address': '上海市长宁区淞虹路661号' },
        { 'value': 'Vim', 'address': '上海市普陀区真北路988号创邑金沙谷6号楼113' },
        { 'value': 'Vscode', 'address': '天山西路438号' }
      ]
    },
    handleSelect (item) {
      console.log(item)
    }
  },
  mounted () {
    this.restaurants = this.loadAll()
  }
}
</script>

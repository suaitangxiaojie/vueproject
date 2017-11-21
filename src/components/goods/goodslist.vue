<template>
    <div class="tmpl">
        <el-row>
            <el-col :span="24">
               <div class="abread bt-line">
                    <el-breadcrumb separator="/">
                            <el-breadcrumb-item :to="{ path: '/' }">购物商城                </el-breadcrumb-item>
                            <el-breadcrumb-item>首页</el-breadcrumb-item>
                            <el-breadcrumb-item>内容管理</el-breadcrumb-item>            </el-breadcrumb>
                </div>
                         
            </el-col>
        </el-row>
        <el-row>
            <el-col :span="24">
              <div class="abread bt-line">
                  <el-row>
                      <el-col :span="6">
                        <el-button>新增</el-button>
                        <el-button>全选</el-button>
                        <el-button>删除</el-button>
                      </el-col>
                      <el-col :offset="14" :span="4">
                          <el-input placeholder="请选择日期" icon="search" v-model="searchValue" :on-icon-click="getlist">
                                
                          </el-input>
                      </el-col>
                  </el-row>                  
               </div>
            </el-col>
        </el-row>
        <el-row>
            <el-col :span="24">
                <el-table ref="multipleTable" :data="list" border tooltip-effect="dark" style="width: 100%">
                <el-table-column type="selection" width="55">
                </el-table-column>
                <el-table-column prop="title" label="标题">
                </el-table-column>
                <el-table-column prop="categoryname" label="所属类别" width="100">
                </el-table-column>
                <el-table-column prop="stock_quantity" label="库存" width="100">
                </el-table-column>
                <el-table-column prop="market_price" label="市场价" width="100">
                </el-table-column>
                <el-table-column prop="sell_price" label="销售价" width="100">
                </el-table-column>
                <el-table-column label="属性" width="120">
                    <template scope="scope">
                       <i v-bind="{class:'el-icon-picture '+(scope.row.is_slide==1?'':'unlinght') }"></i>
                            <i v-bind="{class:'el-icon-upload '+(scope.row.is_top==1?'':'unlinght') }"></i>   
                    </template>
                </el-table-column>
                <el-table-column label="操作" width="120">
                        <template scope="scope">
                            <a href="#">修改</a>
                        </template>
                    </el-table-column>
            </el-table>
            </el-col>
        </el-row>
        <el-row>
            <el-col :span="24">
                <el-pagination @size-change="pageSizeChange"
                 @current-change="pageIndexChange"
                 :current-page="pageIndex" :page-sizes="[1,10, 20, 30, 40]"
                :page-size="pageSize" layout="total, sizes, prev, pager, next, jumper"
                :total="totalCount">
                </el-pagination>
            </el-col>
        </el-row>
    </div>
</template>

<script>
export default {
  data() {
    return {
        pageSize:10,
        pageIndex:1,
        totalCount:0,
        searchValue:'',
        list:[],
        input2:""
    };
  },
  methods: {
      pageIndexChange(currentPage){
          this.pageIndex = currentPage;
          this.getlist();
      },
      pageSizeChange(size){
          this.pageSize = size;
          this.getlist();
      },
      getlist(){
          var url = '/admin/goods/getlist?pageIndex='+this.pageIndex+'&pageSize='+this.pageSize+'&searchvalue=' + this.searchValue;
          this.$ajax.get(url).then(res=>{
              this.list = res.data.message;
              this.totalCount = res.data.totalcount;
          });
      }
  },
  mounted() {
      this.getlist();
  }
};
</script>
<style scoped>

</style>

<style scoped>

.unlinght{
     color:rgba(0,0,0,0.3);
 }

</style>
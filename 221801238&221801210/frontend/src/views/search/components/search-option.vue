<template>
  <div class="search_option">
    <div class="left">
      <div class="top">
        <el-radio-group v-model="searchOption.searchMethod">
          <el-radio :label="1">在已有结果上搜索</el-radio>
          <el-radio :label="2">重新搜索</el-radio>
        </el-radio-group>
        <span class="search_total">为您搜索到{{ total }}个论文</span>
      </div>
      <div class="bottom">
        <el-radio-group class="search_order" v-model="searchOption.sortOrder" size="mini">
          <el-radio-button :label="1">出版日期升序</el-radio-button>
          <el-radio-button :label="2">出版日期降序</el-radio-button>
          <el-radio-button :label="3">查看量</el-radio-button>
        </el-radio-group>
        <el-pagination background layout="prev, pager, next" :total="(parseInt(total/10) + 1 ) * 10" @current-change="changePage"/>
      </div>
    </div>
    <div class="right">
      <div class="square-button">
        <i class="el-icon-s-data button-icon"/>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "search-option",
  props: {
    total: {
      type: Number
    }
  },
  data() {
    return {
      searchOption: {
        searchMethod: 1,
        selectMode: true,
        sortOrder: 1
      }
    }
  },
  methods: {
    changePage(page) {
      this.$api.Paper.page(page - 1).then(res => {
        this.$store.commit('setPaperList', res.data.data.paperList)
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.search_option {
  color: rgba(176, 176, 176, 100);
  font-size: 14px;
  margin-left: 80px;
  margin-top: 10px;
  width: 910px;
  display: flex;
  justify-content: space-between;

  .search_total {
    margin-left: 16px;
  }

  .search_order {
    margin-left: 10px;
  }

  .bottom {
    margin-top: 10px;
    display: flex;
    align-items: center;
  }
}

.right {
  display: flex;
}

.square-button {
  border-radius: 4px;
  background-color: rgba(78, 110, 242, 100);
  width: 62px;
  height: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-left: 20px;

  .button-icon {
    font-size: 41px;
    color: white;
  }
}
</style>
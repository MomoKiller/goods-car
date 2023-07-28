<template>
  <div class="manage-wrap">
    <section class="no-data" v-if="manageList.length == 0">
      暂无数据
    </section>
    <section v-else>
      <ul 
        class="manage-ul"
      >
        <li 
          v-for="item in manageList" 
          :key="item.id"
          class="goods-list"
        >
          <div class="name">{{ item.name }}</div>
          <div class="price">{{item.price}}*{{item.count}}</div>
          <button @click="delGoodHandler(item)">删除</button>
        </li>
      </ul>
      <button class="btn-buy" @click="buyAllHandler">购买</button>
    </section>
  </div>
</template>

<script>

import { toRefs } from 'vue';
export default {
  name: 'CarManage',
  props: {
    manageList: []
  },
  
  setup(props) {

    const { manageList } = toRefs(props)

    const delGoodHandler = (goods) => {
      
      const goodsIndex = manageList.value.findIndex(item=> item.id == goods.id)
      if(goods.count <=1) {
        confirm(`确定要移除${goods.name}吗？`) && manageList.value.splice(goodsIndex, 1)
      }else{
        manageList.value[goodsIndex].count -= 1
      }
    }

    const buyAllHandler = () => {
      const allSpance = manageList.value.reduce((sum, item)=> {
        let { count, price } = item
        // return sum += count * price
        sum = parseFloat((sum + (count * price)).toFixed(10)) // 小数精度
        return sum
      }, 0)

      alert(`总共消费${allSpance}元`)
    }

    return {
      delGoodHandler,
      buyAllHandler
    }

  }

}
</script>

<style scoped>
.manage-wrap{
  width: 200px;
  min-height: 200px;
  max-height: 400px;
  padding: 8px;
  background-color: #fff;
  box-shadow: 0px 0px 2px 1px #666;
  position: absolute;
  top: 21px;
  right: 0;
}

.no-data {
  height: 160px;
  line-height: 160px;
  text-align: center;
}
.manage-ul {
  /* height: 180px; */
  overflow-y: auto;
  min-height: 160px;
  max-height: 300px;
}
.goods-list {
  height: 38px;
  line-height: 38px;
  display: flex;
  align-items: center;
  justify-content: center;
  
}
.name {
  flex: 1;
  overflow:hidden;
	text-overflow:ellipsis; 
	-o-text-overflow:ellipsis;
	white-space:nowrap;
	width:100%;
  text-align: left;
}
.price{
  margin-right: 8px;
}

.btn-buy {
  width: 100%;
  margin-top: 8px;
}
</style>
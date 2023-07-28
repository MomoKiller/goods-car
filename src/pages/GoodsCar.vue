<template>
  <div class="container">
    <nav class="car-wrap">
      <h2>购物天堂</h2>
      <button 
        class="manage-button"
      >
        购物车
        <CarManage 
          class="car-manage"
          :manageList="manageList"
        ></CarManage>
      </button>
    </nav>

    <ul class="goods-wrap">
      <li 
        v-for="item in goodsList" 
        :key="item.id"
        class="goods-list"
      >
        <div class="goods-img">
          <img :src="item.img" alt="...">
        </div>
        <div class="goods-detail">
          <div class="name">{{item.name}}</div>
          <div class="price">{{item.price}}</div>
          <button 
            @click="pushToCarHandler(item)"
            class="btn"
          >加入购物车</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue';
import CarManage from '../components/CarManage'

export default {
  name: 'GoodsCar',
  components: {
    CarManage
  },

  setup() {
    
    const goodsList = [
      {
        id: '0001',
        img: require('../assets/logo.png'),
        name: '苹果-线上视频面试（万得3C会议）线上视频面试（万得3C会议）',
        price: 10.99,
      },{
        id: '0002',
        img: '',
        name: '西瓜',
        price: 10.99,
      },{
        id: '0003',
        img: '',
        name: '葡萄',
        price: 10.99,
      },{
        id: '0004',
        img: '',
        name: '海南凤梨',
        price: 10.99,
      },{
        id: '0005',
        img: '',
        name: '北京烤鸭',
        price: 10.99,
      },{
        id: '0006',
        img: '',
        name: '香蕉',
        price: 10.99,
      }
    ]

    const manageList = ref([])   // 购物车列表

    const pushToCarHandler = (goods) => {

      if(manageList.value.some(item => item.id == goods.id)) {
        const goodsIndex = manageList.value.findIndex(item=> item.id == goods.id)
        manageList.value[goodsIndex].count += 1
      }else {
        manageList.value.push({
          ...goods,
          count: 1
        })
      }
    }

    return {
      goodsList,
      manageList,
      pushToCarHandler,
    }
  }

  
}
</script>

<style scoped>
.container{
  max-width: 1200px;
  min-width: 900px;
  margin: 0 auto;
  padding-bottom: 50px;
}

.car-wrap {
  height: 60px;
  line-height: 60px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
  z-index: 999;
}

.goods-wrap {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); 
  grid-gap: 8px;
}

.goods-list{
  /* margin: 8px; */
  padding: 8px;
  box-shadow: 0px 0px 2px 1px #666;
}


.goods-list:hover{
  box-shadow: 0px 0px 4px 2px #666;
}

.goods-img{
  width: 100%;
  height: 0;
  padding-bottom: 100%;
  background-color: #efefef;
  position: relative;
}

.goods-img img {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.goods-detail {
  height: 38px;
  line-height: 38px;
  margin-top: 8px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.name{
  flex: 1;
  overflow:hidden;
	text-overflow:ellipsis; 
	-o-text-overflow:ellipsis;
	white-space:nowrap;
	width:100%;
}
.price{
  margin-right: 8px;
}

.manage-button {
  position: relative;
  cursor: pointer;
}
.manage-button .car-manage {
  display: none;
}
.manage-button:hover .car-manage {
  display: block;
}
</style>
<template>
<div>
<div class='text-right mt-4'>
    <button class="btn btn-warning">建立新的產品</button>
</div>
<table class="table mt-4">
<thead>
<tr>
    <th width='120'>分類</th>
    <th>產品名稱</th>
    <th width='120'>原價</th>
    <th width='120'>售價</th>
    <th width='100'>是否啟用</th>
    <th width='80'>編輯</th>
</tr>
</thead>
<tbody>
<tr v-for='(item) in products' :key='item.id'>
<td>{{item.category}}</td>
<td>{{item.title}}</td>
<td class='text-right'>
{{item.origin_price}}
</td>
<td class='text-right'>{{item.price}}</td>
<td>
<span v-if='item.is_enabled' class='text-success'>啟用</span>
<span v-else>未啟用</span>
</td>
<td>
<button class="btn btn-primary  btn-sm">編輯</button>
</td>


</tr>
</tbody>
</table>
</div>
</template>


<script>
//匯出給其他元件使用
export default {
    data(){
        return{
            products:[],
        };
},
methods:{
    getproducts(){
        const api =`${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/products`; //定義成環境變數
        const vm =this;
    //'https://vue-course-api.hexschool.io/api/echo/products';
    //API伺服器路徑
    //所申請的APIPATH
     console.log(process.env.APIPATH,process.env.CUSTOMPATH)
     this.$http.get(api).then((response) => {
     console.log(response.data)
     vm.products=response.data.products
});
    },
},
created() {
    this.getproducts();
},
};
</script>
<template>
<div class="container-fluid">
        <div class="row" id="particles" style="position: absolute;top:0px;width: 100%;height: 99%;background: #99CCFF">
        </div>
        <div id="list" class="row text-center">
            <div class="col-md-2">
                <h1>{{list.name}}</h1>
            </div>
            <div class="col-md-2">
                <h3><small class="a"></small></h3>
            </div>
            <div class="col-md-2">
                <h3><small></small></h3>
            </div>
            <div class="col-md-2">
                <h3><small></small></h3>
            </div>
            <div class="col-md-2">
                <h3><small></small></h3>
            </div>
            <div class="col-md-2">
                <h3><small></small></h3>
            </div>
        </div>
        <div class="row" style="margin-top: 10%;">
            <form>
            <div class="col-md-6 col-md-offset-3" style="margin-bottom: 1%">
                <input v-model="name"  style="height: 50px;background: white;border-color: #46b8da;font-size: 16px; color: black"
                    type="text" class="form-control text-center" placeholder="请输入电影名称">
            </div>
            <div class="col-md-6 col-md-offset-3">
                <button style="width: 100%;height: 50px;" type="button" v-on:click="greet()"
                    class="btn btn-info">搜&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;索</button>
            </div>
        </form>
        </div>
        <div class="row text-center" style="margin-top: 3%">
            <div class="col-md-6 col-md-offset-3">
                <table class="table table-bordered">
                    <tr>
                        <td style="background: #5bc0de;border-color: #46b8da;font-size: 16px; color: white;padding:10px;">
                            搜&nbsp;&nbsp;索&nbsp;&nbsp;结&nbsp;&nbsp;果</td>
                    </tr>
                    <tr v-for="dianyin in list" :key="dianyin.num">
                        <td style="background: white;border-color: #46b8da;font-size: 16px; color: black;padding:10px;">
                        <a v-bind:href="dianyin.url">{{dianyin.name}}</a>
                            </td>
                    </tr>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      name:"",
      title: 'TOPROOTMAN',
      list:[]
    }
  },
  methods:{
      greet: function (event) {
        var value = {
            name:this.name,
        };
        var that = this;
        $.ajax({ 
            type : "POST", 
            url : "http://localhost:9999/data/search.do?pageNum=1&pageSize=10", 
            data : JSON.stringify(value), 
            contentType : "application/json", 
            dataType : "json", 
            complete : function(data) { 
                that.list= JSON.parse(data.responseText).rows
                console.log(that.list)
            } 
        }); 
        that.$forceUpdate();
    }
  }
  
}
</script>

<style>
#app {

}
</style>

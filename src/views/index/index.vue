<template>
  <div class="body">
    <div class="center">
        <div class="nav">
            <div class="left">
                TMK
            </div>
            <div class="right">
                <ul>
                    <li><a href="#">首页</a></li>
                    <li><a href="#zp">作品</a></li>
                    <li><a href="#bj">笔记</a></li>
                    <li><a href="#ly">旅游</a></li>
                    <li><a href="" style="border: none;">关于</a></li>
                </ul>
            </div>
        </div>
        <div class="banner">
            <h1>小凯的博客</h1>
            <p>2025年12月6日13:24:00</p>
        </div>
        <!-- 作品 -->
        <div class="box" id="zp">
            <div class="hard">
                <div class="left">
                    <span>作品</span>
                </div>
                <div class="right">
                    <!-- <a href="">></a> -->
                    <router-link to="/works">></router-link>
                </div>
            </div>
            <div class="body">
                <a :href="item.label" v-for="item in workslist" :key="item.id">
                    <div class="cart" >
                        <div class="img">
                            <img src="../../assets/avatar.jpg" alt="">
                        </div>
                        <div class="box">
                            <span style="color: red;">{{ item.title }}</span>
                            <span><svg t="1763739628070" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="5952"><path d="M512 73.142857C269.604571 73.142857 73.142857 269.604571 73.142857 512s196.461714 438.857143 438.857143 438.857143 438.857143-196.461714 438.857143-438.857143S754.395429 73.142857 512 73.142857z m0-73.142857c282.770286 0 512 229.229714 512 512s-229.229714 512-512 512S0 794.770286 0 512 229.229714 0 512 0z" fill="#666666" p-id="5953"></path><path d="M521.142857 182.857143C495.908571 182.857143 475.428571 203.337143 475.428571 228.571429V548.571429a45.714286 45.714286 0 0 0 91.428572 0V228.571429c0-25.234286-20.48-45.714286-45.714286-45.714286z" fill="#666666" p-id="5954"></path><path d="M523.337143 507.611429a45.714286 45.714286 0 0 0-32.292572 78.043428l165.778286 160.548572a45.714286 45.714286 0 0 0 64.621714-64.585143l-165.778285-160.621715a45.568 45.568 0 0 0-32.329143-13.385142z" p-id="5955"></path></svg> 
                                {{ item.time }} 
                            </span>
                            <span>{{ item.technology }}</span>
                        </div>
                    </div>
                </a>
            </div>
        </div>
        <!-- 笔记 -->
        <div class="box" id="bj">
            <div class="hard">
                <div class="left">
                    <span>笔记</span>
                </div>
                <div class="right">
                    <router-link to="/notes">></router-link>
                </div>
            </div>
            <div class="body">
                <a :href="item.label" v-for="item in noteslist" :key="item.id">
                    <div class="cart" >
                        <div class="img">
                            <img src="../../assets/avatar.jpg" alt="">
                        </div>
                        <div class="box">
                            <span style="color: red;">{{ item.title }}</span>
                            <span><svg t="1763739628070" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="5952"><path d="M512 73.142857C269.604571 73.142857 73.142857 269.604571 73.142857 512s196.461714 438.857143 438.857143 438.857143 438.857143-196.461714 438.857143-438.857143S754.395429 73.142857 512 73.142857z m0-73.142857c282.770286 0 512 229.229714 512 512s-229.229714 512-512 512S0 794.770286 0 512 229.229714 0 512 0z" fill="#666666" p-id="5953"></path><path d="M521.142857 182.857143C495.908571 182.857143 475.428571 203.337143 475.428571 228.571429V548.571429a45.714286 45.714286 0 0 0 91.428572 0V228.571429c0-25.234286-20.48-45.714286-45.714286-45.714286z" fill="#666666" p-id="5954"></path><path d="M523.337143 507.611429a45.714286 45.714286 0 0 0-32.292572 78.043428l165.778286 160.548572a45.714286 45.714286 0 0 0 64.621714-64.585143l-165.778285-160.621715a45.568 45.568 0 0 0-32.329143-13.385142z" p-id="5955"></path></svg> 
                                {{ item.time }} 
                            </span>
                            <span>{{ item.technology }}</span>
                        </div>
                    </div>
                </a>
            </div>
        </div>
        <!-- 旅游 -->
        <div class="box" id="ly">
            <div class="hard">
                <div class="left">
                    <span>旅游</span>
                </div>
                <div class="right">
                    <router-link to="/travel">></router-link>
                </div>
            </div>
            <div class="body">
                <a :href="item.label" v-for="item in travellist" :key="item.id">
                    <div class="cart" >
                        <div class="img">
                            <img src="../../assets/avatar.jpg" alt="">
                        </div>
                        <div class="box">
                            <span style="color: red;">{{ item.name }}</span>
                            <span><svg t="1763739628070" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="5952"><path d="M512 73.142857C269.604571 73.142857 73.142857 269.604571 73.142857 512s196.461714 438.857143 438.857143 438.857143 438.857143-196.461714 438.857143-438.857143S754.395429 73.142857 512 73.142857z m0-73.142857c282.770286 0 512 229.229714 512 512s-229.229714 512-512 512S0 794.770286 0 512 229.229714 0 512 0z" fill="#666666" p-id="5953"></path><path d="M521.142857 182.857143C495.908571 182.857143 475.428571 203.337143 475.428571 228.571429V548.571429a45.714286 45.714286 0 0 0 91.428572 0V228.571429c0-25.234286-20.48-45.714286-45.714286-45.714286z" fill="#666666" p-id="5954"></path><path d="M523.337143 507.611429a45.714286 45.714286 0 0 0-32.292572 78.043428l165.778286 160.548572a45.714286 45.714286 0 0 0 64.621714-64.585143l-165.778285-160.621715a45.568 45.568 0 0 0-32.329143-13.385142z" p-id="5955"></path></svg> 
                                {{ item.time }} 
                            </span>
                            <span>{{ item.description }}</span>
                        </div>
                    </div>
                </a>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            workslist: [],
            noteslist: [],
            travellist: []
        }
    },
    async created() {
    try {
        const res = await axios.get('http://47.79.40.65:3006');
        console.log("后端数据：", res.data);
        // 作品
        // 1. 检查 res.data.works 是否存在且为数组
        if (res.data && res.data.works && Array.isArray(res.data.works)) {
            // 2. 排序 (假设 time 是数字类型)
            const sortedWorks = res.data.works.sort((a, b) => {
                return new Date(b.time).getTime() - new Date(a.time).getTime(); // Sort in descending order (newest first)
            });
             const firstThreeWorks = sortedWorks.slice(0, 4);
            // 4. 赋值给 this.list
            this.workslist = firstThreeWorks;
        }
        // 笔记
        if (res.data && res.data.notes && Array.isArray(res.data.notes)) {
            // 2. 排序 (假设 time 是数字类型)
            const sortednotes = res.data.notes.sort((a, b) => {
                return new Date(b.time).getTime() - new Date(a.time).getTime(); // Sort in descending order (newest first)
            });
             const firstThreenotes = sortednotes.slice(0, 4);
            // 4. 赋值给 this.list
            this.noteslist = firstThreenotes;
        }
         else {
            console.warn("后端返回的数据格式不正确，无法排序和截取。");
            // this.list = []; // 防止出错，赋值为空数组
        }
        // 旅游
        if (res.data && res.data.travel && Array.isArray(res.data.travel)) {
            // 2. 排序 (假设 time 是数字类型)
            const sortedtravel = res.data.travel.sort((a, b) => {
                return new Date(b.time).getTime() - new Date(a.time).getTime(); // Sort in descending order (newest first)
            });
             const firstThreetravel = sortedtravel.slice(0, 4);
            // 4. 赋值给 this.list
            this.travellist = firstThreetravel;
        }
         else {
            console.warn("后端返回的数据格式不正确，无法排序和截取。");
            // this.list = []; // 防止出错，赋值为空数组
        }
    } catch (error) {
        console.error("请求失败:", error); // 打印更详细的错误信息
    }
}
}
</script>

<style scoped>
.body{
    width: 100%;
    /* 方格背景 */
    background: linear-gradient(90deg, rgba(200, 200, 200, 0.1) 3%, transparent 0),
    linear-gradient(rgba(200, 200, 200, 0.1) 3%, transparent 0);
    background-size: 20px 20px;
}
/* nav */
.center{
    width: 80%;
    /* max-width: 1000px; */
    margin: 0 auto;
    padding: 20px;
    font-family: Arial, sans-serif;
    background-color: #fff;
}
.body .nav{
    display: flex;
    justify-content: space-between;
}
.body .nav .left{
    width: 50px;
    height: 50px;
    background-color: #fff;
    border-radius: 50%;
    text-align: center;
    line-height: 50px;
}
.body .nav .right ul{
    list-style: none;
}
.body .nav .right ul li{
    float: left;
}
.body .nav .right ul li a{
    display: block;
    text-decoration: none;
    width: 60px;
    font-size: 18px;
    border-right: 1px solid black;
    text-align: center;
}
/* banner */
.banner{
    width: 100%;
    height: 300px;
    margin-top: 10px;
    text-align: center;
    /* border: 1px solid red; */
    background: url(../../assets/avatar.jpg) left;
    background-repeat:no-repeat;
    background-size:cover; 
    color: red;
}
.banner h1{
    margin-top: 100px;
}
/* box */
.body .box{
    width: 100%;
    /* height: 500px; */
    margin-top: 30px;
    /* border: 1px solid rgb(0, 26, 255); */
    background-color: #fff;
}
.body .box .hard{
    height: 20%;
    background-color: #fff;
    display: flex;
    justify-content: space-between;
    font-size: 30px;
}
.body .box .hard .right a{
    display: block;
    width: 45px;
    height: 45px;
    border-radius: 50%;
    /* border: 1px solid red; */
    text-align: center;
    text-decoration: none;
    line-height: 45px;
    /* background-color: #f3f2f2; */
}
.body .box .hard .right a:hover{
    color: red;
}
.body .box .body{
    margin-top: 10px;
    background-color: #fff;
    font-size: 30px;
    max-width: 1800px;/* 最大高度 */
    overflow-x: auto;/* 水平滚动条 */
}
.body .box .body .cart{
    float: left;
    height: 450px;
    width: 350px;
    border: 1px solid rgb(197, 196, 196);
    margin-right: 25px;
}
.body .box .body .cart:hover{
    box-shadow: 10px 30px 20px -2px rgb(197, 196, 196);
}
.body .box .body .cart .img{
    height: 75%;
    text-align: center;
    align-items: center;
}
.body .box .body .cart .img img{
    width: 100%;
    height: 100%;
}
.body .box .body .cart .box{
    display: flex;
    flex-direction: column;
}
.body .box .body .cart .box span{
    font-size: 20px;
    color: #989898;
}
.body .box .body .cart .box span .icon{
    width: 15px;
    height: 15px;
}
</style>
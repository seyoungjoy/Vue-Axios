<template>
    <div>
        <ul class="list">
            <!-- <li></li> -->
        </ul>
        <input v-model="namaData" placeholder="이름을 입력해주세요">
        <input v-model="jobData" placeholder="직업을 입력해주세요">
        <button @click="test">제출하기</button>

        
    </div>
</template>

<script>
import axios from "axios"

export default{
    data(){
        return{
            contentsdata:null,
            namaData:null,
            jobData:null
            
        }
    },
    methods:{
        test(){
            axios
            .post("https://reqres.in/api/users",{
                name:this.namaData,
                job:this.jobData,
                id:21
            })
            .then(res =>{
                console.log(res.data)
            })
            
            
            
        }
    },
    mounted(){
        let emailList = document.querySelector('.list');
        axios
            .get("https://reqres.in/api/users?page=2")
            .then(res => {

                this.contentsdata = res.data.data; 
                this.contentsdata.forEach((item,idx) => {
                    let {email} = item;
                    emailList.insertAdjacentHTML('beforeend', `<li><a href="/api/${idx}">'${email}'</a></li>`)   
                })
            })
            .catch(err => {
                console.log(err);
        })
    }

}
</script>

<template>
    <div>
        <button @click="test">testttt</button>
        <ul class="list">
            <!-- <li></li> -->
        </ul>
    </div>
</template>

<script>
import axios from "axios"

export default{
    data(){
        return{
            contentsdata:null
            
        }
    },
    methods:{
        test(){
            console.log(11)
            
        }
    },
    mounted(){
        let emailList = document.querySelector('.list');
        axios
            .get("https://reqres.in/api/users?page=2")
            .then(res => {
                this.contentsdata = res.data.data; 
                this.contentsdata.forEach((item,idx) => {
                    let {email,id=idx} = item;
                    emailList.insertAdjacentHTML('beforeend', `<li><a href="/api/${id}">'${email}'</a></li>`)   
                })
            })
            .catch(err => {
                console.log(err);
        })
    }

}
</script>


<template>
<div>
    <HeaderView/>
    
    <div class="container-fluid">
        <h1 style="font-size:3rem;color:white;">Welcome to Update Courses Page</h1>
        <div class="row">
            <div class="col-lg-4"></div>
            <div class="col-lg-4">
                <form @submit.prevent="handleUpdateForm">
        
        <div class="mt-3">
            <label class="fs-5 fw-bold text-white text-right">Enter Name</label>
            <input v-model="course.name" type="text" name="name" placeholder="Enter Name of the Course">
        </div>
        <div class="mt-3">
            <label class="fs-5 fw-bold text-white text-right">Enter Description</label>
            <input v-model="course.description" type="text" name="category" placeholder="Enter Description">
        </div>
        <div class="mt-3">
            <label class="fs-5 fw-bold text-white text-right">Enter Video ID</label>
            <input v-model="course.videoId" type="text" name="videoId" placeholder="Enter Video Id">
        </div>
        <div class="mt-4">
            <button id="updateBTN" class="btn btn-rounded">Update the Course</button>
        </div>
    </form>
            </div>
            <div class="col-lg-4"></div>
        </div>
    </div>
</div>
</template>

<script>
import HeaderView from './HeaderView.vue'
import axios from 'axios'
//const base_url = process.env.base_url
export default{
    name:'UpdateCourses',
    components:{
        HeaderView
    },
    data(){
        return{
            course:{}
        }
    },
    beforeCreate () {
        document.querySelector('body').setAttribute('style', 'background:black')
    },
    methods: {
        handleUpdateForm() {
            ////added local host March 23 2024
            let apiURL = `https://tutormodule-mevn-stack.onrender.com/tutor/update-course/${this.$route.params.id}`;

            axios.post(apiURL, this.course).then((res) => {
                alert("Course Updated Successfully!!")
                console.log(res)
                this.$router.push({name:'DisplayCourses'})
            }).catch(error => {
                console.log(error)
            });
        }
    },
    mounted(){
        let user = localStorage.getItem('user-info');
        if(!user){
            this.$router.push({name:'SignUp'})
        }
    }
}
</script>


<style scoped>
input{
    display: block;
    width:100%;
    padding:1%;
}
label{
    float:left;
}
#updateBTN{
    background:#774c9e;
    display:block;
    width:100%;
    padding:2%;
    color: black;
    font-weight: 800;
}
</style>
<template>
    <div class="creation">
        <Nav/>
        <h1>Create new blog</h1>
        <form class="form-panel" @submit="submitData" method="post">
            <div class="form-group">
                <label for="exampleFormControlInput1">Title</label>
                <input type="text" name='title' v-model="post.title" class="form-control" id="exampleFormControlInput1" placeholder="Please enter title blog"/>
            </div>
            <div class="form-group">
                <label for="exampleFormControlTextarea1">Content</label>
                <textarea class="form-control" name="content" v-model="post.content" id="exampleFormControlTextarea1" rows="3"></textarea>
            </div>
            <div class="form-check">
                <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault1"/>
                <label class="form-check-label" for="flexCheckDefault1">
                    1st classification
                </label>
            </div>
            <div class="form-check">
                <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault2"/>
                <label class="form-check-label" for="flexCheckDefault2">
                    2nd classification
                </label>
            </div>
            <div class="form-check">
                <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault3"/>
                <label class="form-check-label" for="flexCheckDefault3">
                    3rd classification
                </label>
            </div>
            <div class="form-check">
                <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault4"/>
                <label class="form-check-label" for="flexCheckDefault4">
                    4th classification
                </label>
            </div>
            <div class="form-check">
                <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault5"/>
                <label class="form-check-label" for="flexCheckDefault5">
                    5th classification
                </label>
            </div>
            <button type="submit" >Create</button>
        </form>
    </div>
</template>

<script>
	import Nav from "./nav";
	import store from '../../store';
	import {uuid} from 'vue-uuid';
	import Vue from 'vue';
	// import axios from 'axios';

	export default {
		name: 'Create',
		components: {Nav},
		data(){
			return{
				post:{
					title:null,
					content:null,
					uuid: uuid.v1(),
					id: null
                }
            }
        },
        methods:{
			submitData(e){
				e.preventDefault();

				const newID = this.$uuid.v4();
				const userId = this.$uuid.v1();
				const obj = {
					body: this.post.content,
					title: this.post.title,
					id: newID,
					userId
				};

				// store.dispatch("", obj)
				Vue.axios.post('https://jsonplaceholder.typicode.com/posts' , obj)
					.then(res => {
						store.dispatch("pushBlog",obj);
						console.log(res);

					})
			},

        }
	}
</script>

<style>
    h1{
        text-align: center;
    }
    .form-panel{
        width: 350px;
        background-color: #2c3e50;
        color: #d0d0d0;
        display: block;
        padding: 10px;
        border-radius: 10px;
        margin: 50px auto;
    }
</style>



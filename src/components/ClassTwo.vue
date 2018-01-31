<template>
  <div class="col-sm-6 col-xs-12">
    <h1>Class #2</h1>
    <ul class="list-group">
      <li class="list-group-item" v-for="(student, index) in students">{{ student }} <br> <button class="btn btn-info" @click="returnBack(student, index)">Return to School</button> <button class="btn btn-warning" @click="moveToClassOne(student, index)">Move to #1</button> <button class="btn btn-danger" @click="removeStudent(student, index)">Leave School</button></li>
    </ul>
  </div>
</template>

<script>
import { bus } from '../main';

export default {
  props: ['student'],
	data: function(){
  	return {
    	students: [],
    }
  },
  watch: {
  	student: function(student){
    	this.students.push(student);
    }
  },
  methods: {
  	returnBack: function(student, index){
    	this.students.splice(index, 1);
      this.$emit('return', student);
    },
    moveToClassOne: function(student, index){
    	this.$emit('increase', 1);
      this.$emit('decrease', 2);
    	bus.$emit('is-moved-one', student);
      this.students.splice(index, 1);
    },
    removeStudent: function(student, index){
    	this.students.splice(index, 1);
      this.$emit('decrease', 2);
    },
    moved: function(student){
    	this.students.push(student);
    }
  },
  created: function(){
  	bus.$on('is-moved-two', this.moved);
  }
}
</script>

<style>

</style>

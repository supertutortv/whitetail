<template>
<div class="cms-div">
		<h5>Add a Course </h5>
        <h4>Course<input title="CourseTitle" v-model="course_object.course"></h4>
        <ul class="entry-list" v-for="(subject, index) in course_object.subjects">
            <li>Subject: <input title="Subject" v-model="subject.title"></li>
            <li>
                <ul v-for="(entry, index) in subject.entries">
                    <li><strong>Entry: </strong></li>
                    <li>Name <input title="Name" v-model="entry.name"></li>
                    <li>ID <input title="ID" v-model="entry.id"></li>
            	<button class="button btn-secondary" @click="addEntry(subject.entries)">Add Entry</button>
                <button v-if="subject.entries.length > 1" v-on:click="removeEntry(subject.entries, index);" style="cursor: pointer">Remove Entry</button>
            	<li>
                	<button class="remove-subject-button" v-if="course_object.subjects.length > 1" v-on:click="removeSubject(index);" style="cursor: pointer">Remove Subject</button>
            	</li>
                </ul>
            </li>
        </ul>

    <div>
        <button class="button btn-primary" @click="addSubject">Add Subject</button>
    </div>
    <p> {{course_object}} </p>
</div>
</template>

<script>
    const Vue = require('vue');
    const fs = Vue.use('fs');
    export default{
        data() {
            return {
                course_object : {course : "",
                        subjects: [{ "title": "", "entries": [{ "name": "", "id": "" }]}]},
            }
        },
        methods: {
            addSubject: function() {
                let elem = document.createElement('li');
                this.course_object.subjects.push({
                    title: "",
                    entries: [ { "name": "", "id": "" } ]
                });
            },
            removeSubject: function(index) {
                this.course_object.subjects.splice(index, 1);
            },
            addEntry: function(item){
                let elem = document.createElement('li');
                item.push({
                    name: "",
                    id: ""
                })
            },
            removeEntry: function(item, index){
                item.splice(index, 1)
            }
        }
    }
</script>

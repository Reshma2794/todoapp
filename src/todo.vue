<template>
    <div class="container">
        <h1> TodoList </h1>

            <input type="text"  v-model="new_item" @keyup.enter="add_item" placeholder="Please input your task"
            />
            <button type="submit" @click="add_item">Add </button>



        <div class='content'  v-for="(list,index) in taskList">

            <ul>
                <li>
                    <span> <editable :value.sync="list.name" style="max-width:350px !important;"> </editable></span>
                    <span class="fa fa-trash" @click="remove(index)" id="trash"  data-toggle="tooltip" title="Remove" >  </span>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    import Editable from './Editable.vue'
    export default
    {

        components:
            {
                'editable': Editable,

            },
        data()
            {
              return{
                  new_item:'',
                  taskList:[
                      {
                          name:'finish presentation'
                      },
                      {
                          name:'arrange the books'
                      },
                      {
                          name:'cook for lunch'
                      },
                  ],
              }
            },
        methods:
            {
                add_item()
                {
                    if(this.new_item=='')
                    {
                        swal({
                            title: "Oops!",
                            text: "Please input yout task",
                            icon: "error",
                            button: "Ok",
                        });
                    }
                    else {
                        this.taskList.push({'name': this.new_item});
                        this.new_item = '';
                    }
                },
                remove(index)
                {
                    this.$delete(this.taskList,index);
                }
            },
    }
</script>
<style>
    .container
    {
        margin-top:10px;

    }
    ul
    {
        list-style:none;
    }

    input
    {
        margin-top:20px;
        width:450px;
        position: relative;
        left:30px;
        padding:5px;
    }
    button
    {
       width:100px;
        padding:5px;
        margin-left:50px;
        background-color:white;
        border:2px solid mediumseagreen;
    }
    .content
    {
        text-align: left;
        top:10px;
    }


    </style>
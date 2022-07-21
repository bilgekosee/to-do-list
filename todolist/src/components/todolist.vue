<template>
  <div class="container" style="max-width:600px">

    <h3 class="text-center mt-5">Benim Mükemmel Yapılacaklar Listem</h3>

    <div class="d-flex">
      <input type="text"  v-model="task" placeholder="enter task" class="w-100 from-control">
      <button  class="btn btn-warning rounded-0" @click="submitTask">EKLE</button>
    </div>

    <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Liste</th>
      <th scope="col">Durum</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>

    <tr v-for="(task, index) in tasks" :key="index">
      <td>
       <span :class="{'line-through' : task.status === 'yapıldı'}">{{task.name}}</span> 
      </td>
      <td style="width: 220px">
        <span  class="pointer noselecet" @click="changeStatus(index)"
         :class="{'text-danger': task.status === 'yapılacak',
         'text-warning': task.status === 'devam ediliyor',
         'text-success': task.status === 'yapıldı'}"
        >
        {{capitalizeFirstCharUpper(task.status)}}
        </span>
      </td>
      <td class="text-center">
        <div @click="deleteTask(index)">
          <span class="fa fa-trash pointer"></span>
        </div>
      </td>
      <td class="text-center">
         <div @click="editTask(index)">
          <p class="fa fa-pen pointer"></p>
        </div>
      </td>
    </tr>
  </tbody>
</table>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return{
      task: "",
      editedTask: null,
      statues: ['yapılacak', 'devam ediliyor','yapıldı'],

      tasks:[{
        name: 'yaşamak için birkaç sebep bulmak.',
        status: 'yapılacak'
      },
      {
        name: 'kitap okumak',
        status: 'devam ediliyor'
      },
      {
        name: 'anime izle.',
        status: "yapıldı"
      },
      
      
      ],
    }
  },
  methods:{

    capitalizeFirstCharUpper(str){
      return str.charAt(0).toUpperCase() + str.slice(1);
    },

    changeStatus(index){
      // eslint-disable-next-line no-unused-vars
      let newIndex= this.statues.indexOf(this.tasks[index].status);
      if(++newIndex > 2) newIndex = 0;
      this.tasks[index].status= this.statues[newIndex];
    },

    deleteTask(index){
      this.tasks.splice(index, 1);
    },

    editTask(index){
      this.task=this.tasks[index].name;
      this.editedTask = index; 
    },

    submitTask(){
      if(this.task.length ===0) return;
      if(this.editedTask != null)
      {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }
      else{
       this.tasks.push({
         name: this.task,
         status: 'yapılacak'
       })
      } 
        
      
      this.task = '';
    }
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pointer {
  cursor: pointer;
}
.noselect {
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Old versions of Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none; /* Non-prefixed version, currently
                                  supported by Chrome, Edge, Opera and Firefox */
}
.line-through {
  text-decoration: line-through;
}
</style>

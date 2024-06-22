<template>
  <div>
    <b-table striped hover :items="items" :fields="fields"></b-table>

    <form @submit.prevent="register">
      <div class="form-group">
        <label for="email">Email</label>
        <input type="email" class="form-control" id="email" v-model="form.email" required>
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input type="password" class="form-control" id="password" v-model="form.password" required>
      </div>
      <button type="submit" class="btn btn-primary">Register</button>
    </form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        items: null,
        fields: ['id', 'USERNAME'],
        form: {
          email: '',
          password: ''
        }
      }
    },
    methods:{
      get_accounts(){
        axios.get('/get_accounts').then(response=>{
          console.log(response.data);
          this.items = response.data;
        }).catch(error=>{
          console.log(error.data);
        })
      },
      register(){
        axios.post('/register/registration', this.form).then(response=>{
          console.log(response.data.email);
          console.log(response.data.password);
          this.items.push(response.data);
        }).catch(error=>{
          console.log(error.data);
          this.loading = false;
        })
      },
    },
    beforeMount(){
      this.get_accounts();
    }
  }
</script>
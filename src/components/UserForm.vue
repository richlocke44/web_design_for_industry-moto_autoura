<template>
    <div class="col-12">
        
        <ul>
        <li v-bind:key="index" v-for="(error, index) in errors">
          {{error}}
        </li>
        <li v-bind:key="index" v-for="(error, index) in parentErrors">
          {{error}}
        </li>
      </ul>
      
      <form @submit="submitForm">
        <div class="form-group">
          <label for="email">Email: *</label>
          <input type="email" 
          class="form-control" 
          id="email" 
          name="email" 
          v-model="email">
        </div>
        
        <div class="form-group" v-if="confEmail">
          <label for="confirmEmail">Confirm Email: *</label>
          <input type="email" 
          class="form-control" 
          id="confirmEmail" 
          name="confirmEmail" 
          v-model="confirmEmail">
        </div>
        
        <div class="form-group">
          <label for="password">Password: *</label>
          <input type="password" 
          class="form-control" 
          id="password" 
          name="password" 
          v-model="password">
        </div>
        
        <button type="submit" class="btn btn-primary">{{buttonText}}</button>
      </form>
    </div>
    
</template>

<script>
    export default {
        name: "UserForm",
        props: {
            confEmail: Boolean,
            parentErrors: Array,
            buttonText: String
        },
        data: function(){
            return {
            email: '2lockr07@solent.ac.uk', 
            confirmEmail: '2lockr07@solent.ac.uk',
            password: 'password',
            errors: []
      };
    }, 
    
    methods: {
        submitForm(e){
        e.preventDefault();
        this.errors = [];
        
        if(this.email && (this.email == this.confirmEmail || !this.confEmail) && this.password) {
          this.$emit('form-submitted', {email: this.email, password: this.password})
        }
        
        if (!this.email) {
          this.errors.push('Please enter an Email');
        }
        
        if(this.email != this.confirmEmail && this.confEmail) {
          this.errors.push('Emails do not match');
        }
        
        if (!this.password) {
          this.errors.push('Please enter a password');
        }
      }
    }
};
    
</script>
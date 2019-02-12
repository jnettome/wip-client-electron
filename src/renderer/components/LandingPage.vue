<template>
  <div id="wrapper" class="logo-screen">
    <mu-container class="demo-container is-stripe">
      <system-information></system-information>
    </mu-container>
    
  </div>
</template>

<script>
  import SystemInformation from './LandingPage/SystemInformation'
  
  export default {
    name: 'landing-page',
    components: { SystemInformation },
    data () {
    return {
      usernameRules: [
        { validate: (val) => !!val, message: 'Username must be filled in'},
        { validate: (val) => val.length >= 3, message: 'Username length greater than 3'}
      ],
      passwordRules: [
        { validate: (val) => !!val, message: 'Password must be filled in'},
        { validate: (val) => val.length >= 3 && val.length <= 10, message: 'Password length must be greater than 3 and less than 10'}
      ],
      argeeRules: [{ validate: (val) => !!val, message: 'Must agree with user agreement'}],
      validateForm: {
        username: '',
        password: '',
        isAgree: false
      }
    }
  },
  methods: {
    submit () {
      this.$refs.form.validate().then((result) => {
        console.log('form valid: ', result)
      });
    },
    clear () {
      this.$refs.form.clear();
      this.validateForm = {
        username: '',
        password: '',
        isAgree: false
      };
    },
    open (link) {
      this.$electron.shell.openExternal(link)
    }
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body { 
    font-family: 'Source Sans Pro', sans-serif; 
    /* background: #666; */
  }

  #wrapper {
    /* background:
      radial-gradient(
        ellipse at top left,
        rgba(33, 33, 33, 1) 40%,
        rgba(00, 00, 00, .9) 100%
      ); */
    background:
      radial-gradient(
        ellipse at top left,
        rgba(255, 255, 255, 1) 40%,
        rgba(99, 99, 99, .9) 100%
      );
    height: 100vh;
    padding: 60px 80px;
    width: 100vw;
  }

  #logo {
    height: auto;
    margin-bottom: 20px;
    width: 420px;
  }

  main {
    display: flex;
    justify-content: space-between;
  }

  main > div { flex-basis: 50%; }
</style>

<template>
    <div>
        <h1>Login</h1>
        <button @click="login('admin')">Login as Admin</button>
        <button @click="login('editor')">Login as Editor</button>
        <button @click="login('viewer')">Login as Viewer</button>
    </div>
</template>

<script>
import {jwtDecode} from 'jwt-decode';

export default {
  name: 'Login',
  methods: {
    login(role){
        let token;
        //Aquí se asigna el token según el rol. En este punto se haría
        //el consumo de la autenticación con el
        //el response con el JWT (token).
        switch (role) {
          case 'admin':
            token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyb2xlIjoiYWRtaW4ifQ.UHnffynBjuE3dcwEUyqldVbN-5QzMT-oiyXqkRbWJOI"
            break;
          case 'editor':
            token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyb2xlIjoiZWRpdG9yIn0.O_uqVbz-BOfRRRmyY5bMX0aEg_YmWESE_okCflsM_JA"
            break;  
          case 'viewer':
            token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyb2xlIjoidmlld2VyIn0.uoNjQeybe0q6NSVYguZLJCpOg7ftV7b_TW76Cp-3euc"
            break;
          default:
            break;
        }

        //Guardar el token en localStorage
        localStorage.setItem('token', token);

        //Decodificar el token para obtener el
        const decoded = jwtDecode(token);
        this.redirectUser(decoded.role);
    },
    redirectUser(role){
      //Redirige al usuario según su rol
      if (role === 'admin') {
        this.$router.push('/admin');
      } else if (role === 'editor') {
        this.$router.push('/editor');
      }
      else if (role === 'viewer') {
        this.$router.push('/viewer');
      }
    }

  }
};
</script>
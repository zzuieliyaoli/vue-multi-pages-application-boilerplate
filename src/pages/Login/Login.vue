<template>
  <div id="login-page">
    <top-Header></top-Header>
    <logo></logo>
    <h2>Login Page</h2>
  </div>
</template>

<script>
import Header from '../../components/Header';
import Logo from '../../components/Logo';

export default {
  name: 'LoginPage',
  components: {
    TopHeader: Header,
    Logo,
  },
};
</script>

<style>
body {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

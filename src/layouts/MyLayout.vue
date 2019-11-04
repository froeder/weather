<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title>
          Previsão do Tempo
        </q-toolbar-title>

      </q-toolbar>
    </q-header>



    <q-page-container>
      <router-view />
    </q-page-container>
    <q-footer style="padding:10px">Developer by: Jhonatan Froeder</q-footer>
  </q-layout>
</template>

<script>
export default {
  name: 'MyLayout',

  data () {
    return {
      leftDrawerOpen: false
    }
  }
}
</script>

<template>
  <div class="localeChanger">

    <v-select
            :items="langs"
            v-model="$i18n.locale"
            single-line
            dense
            style="word-wrap: normal !important;"
            class="pa-4 ma-4"
            
          ></v-select>
   
  </div>
</template>

<script>
export default {
  name: 'localeChanger',
  data () {
    return { langs: ['en', 'ru'] }
  }
}
</script>
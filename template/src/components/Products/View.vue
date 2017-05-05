<template>
  <div>
    <h4>
      Detalhes do produto
      <q-fab
        classNames="dark"
        icon="keyboard_arrow_right"
        direction="right"
      >
        <q-small-fab
            class="white"
            v-link="'/products'"
            icon="arrow_back"
        ></q-small-fab>
        <q-small-fab
            class="primary"
            @click.native="openModal('/products/' + product.id + '/edit')"
            icon="edit"
        ></q-small-fab>
        <q-small-fab
            class="negative"
            @click.native="openModal('/products/' + product.id + '/remove')"
            icon="delete"
        ></q-small-fab>
      </q-fab>
    </h4>

    <q-modal ref="basicModal" position="bottom" :content-css="{minWindth: '800px', minHeight: '100px', padding: '20px'}" @close="closeModal()">
      <router-view></router-view>
      <hr>
      <button class="small primary" @click="$refs.basicModal.close()">Fechar</button>
    </q-modal>

    <table class="q-table horizontal-delimiter striped-even loose">
      <tbody>
      <tr>
        <th>Título</th>
        <td>{{ product.title }}</td>
      </tr>
      <tr>
        <th>Descrição</th>
        <td>{{ product.description }}</td>
      </tr>
      <tr>
        <th>Preço</th>
        <td>{{ product.price | currency }}</td>
      </tr>
      <tr>
        <th>Custo</th>
        <td>{{ product.cost | currency }}</td>
      </tr>
      
      </tbody>
    </table>
    
  </div>
</template>

<script>
export default {
  computed: {
    product () {
      return this.$store.state.products.one.product || {}
    },
    
   methods: {
    openModal (url) {
      this.$router.push(url)
      this.$refs.basicModal.open()
    },
    closeModal () {
      this.$router.push('/products/' + this.product.id)
    }
  },
  mounted () {
    this.$store.dispatch('productsGet', this.$route.params.id)
  }
}
</script>

<style scoped>
  .q-table {
    width: 100%;
  }
  .q-table tbody th {
    text-align: left;
  }
</style>
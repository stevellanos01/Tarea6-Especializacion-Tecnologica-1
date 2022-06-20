<template>
  <div id="product-table">
    <div v-if="!products.length" class="alert alert-info" role="alert">
      No se han agregado productos
    </div>
    <table class="table">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Descripción</th>
          <th>Precio</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(product, index) in products" :key="index">
          <td v-if="editIndex === index">
            <input
              v-model="editableProduct.name"
              type="text"
              class="form-control"
            />
          </td>
          <td v-else>{{ product.name }}</td>
          <td v-if="editIndex === index">
            <input
              v-model="editableProduct.description"
              type="text"
              class="form-control"
            />
          </td>
          <td v-else>{{ product.description }}</td>
          <td v-if="editIndex === index">
            <input
              v-model="editableProduct.price"
              type="number"
              class="form-control"
            />
          </td>
          <td v-else>${{ product.price }}</td>
          <td v-if="editIndex === index">
            <div class="btn-group" role="group">
              <button class="btn btn-success me-2" @click="saveProduct()">
                Guardar
              </button>
              <button class="btn btn-danger me-2" @click="editIndex = -1">
                Cancelar
              </button>
            </div>
          </td>

          <td v-else>
            <div class="btn-group" role="group">
              <button
                class="btn btn-primary me-2"
                @click="editProduct(product, index)"
              >
                Editar
              </button>
              <button
                class="btn btn-danger me-2"
                @click="$emit('delete-product', index)"
              >
                Eliminar
              </button>
            </div>
          </td>
        </tr>

        <div class="row">
          <div class="col-md-12">
            <div v-if="error" class="alert alert-danger" role="alert">
              ¡Debes rellenar todos los campos!
            </div>
            <div v-if="errorNum" class="alert alert-danger" role="alert">
              ¡Debes ingresar un numero valido!
            </div>
            <div v-if="sent" class="alert alert-success" role="alert">
              El producto ha sido agregada correctamente!
            </div>
          </div>
        </div>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  name: "product-table",
  components: {},

  data() {
    return { editableProduct: {}, editIndex: -1 };
  },
  props: {
    products: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    saveProduct() {
      if (
        this.editableProduct.name.length < 1 ||
        this.editableProduct.description.length < 1 ||
        this.editableProduct.price < 1
      ) {
        return;
      }
      this.$emit("update-product", this.editIndex, this.editableProduct);
      this.editIndex = -1;
    },
    editProduct(product, index) {
      this.editableProduct = Object.assign({}, product);
      this.editIndex = index;
    },
  },
};
</script>

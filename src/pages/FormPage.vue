<template>
  <q-page padding>
    <h4>Agregar Producto</h4>

    <pre>{{ producto }}-{{ seleccion }}-{{ terminos }}</pre>

    <q-form
      class="row q-col-gutter-md"
      @submit.prevent="procesarFormulario"
      @reset="reset"
      ref="myForm"
    >
      <div class="col-12 col-sm-6">
        <q-input
          label="Producto"
          v-model="producto"
          :rules="[
            (val) => (val && val.length > 0) || 'Por favor escribe algo!!',
          ]"
          lazy-rules
        />
      </div>
      <div class="col-12 col-sm-6">
        <q-select
          label="Prioridad"
          v-model="seleccion"
          :options="opciones"
          :rules="[
            (val) => (val && val.length > 0) || 'Por favor elije algo!!',
          ]"
          lazy-rules
        />
      </div>
      <div class="col-12">
        <q-toggle v-model="terminos" label="Acepta los terminos" />
      </div>
      <div class="col-12">
        <q-btn label="Submit" color="primary" type="submit" />
        <q-btn
          label="Reset"
          color="primary"
          outline
          class="q-ml-sm"
          :ripple="false"
          type="reset"
        />
      </div>
    </q-form>

    <mostrar-datos :productos="productos" />
  </q-page>
</template>

<script>
import { useQuasar } from "quasar";
import { ref } from "vue";
import MostrarDatos from "src/components/MostrarDatos.vue";
export default {
  components: { MostrarDatos },
  setup() {
    const $q = useQuasar();
    const producto = ref(null);
    const seleccion = ref(null);
    const myForm = ref(null);
    const terminos = ref(false);
    const opciones = ["maxima", "moderada", "minima"];
    const productos = ref([]);

    const procesarFormulario = () => {
      console.log("Me diste click al formulario");
      if (terminos.value === false) {
        $q.notify({
          color: "red-5",
          textColor: "white",
          icon: "warning",
          message: "Necesitas aceptar los terminos",
        });
      } else {
        $q.notify({
          color: "green-4",
          textColor: "white",
          icon: "cloud_done",
          message: "Enviado",
        });
        myForm.value.resetValidation();
        productos.value = [
          ...productos.value,
          {
            producto: producto.value,
            prioridad: seleccion.value,
          },
        ];
        reset();
        //procesar el formulario
      }
    };
    const reset = () => {
      producto.value = null;
      seleccion.value = null;
      terminos.value = false;
    };
    return {
      producto,
      seleccion,
      opciones,
      procesarFormulario,
      terminos,
      reset,
      myForm,
      productos,
    };
  },
};
</script>

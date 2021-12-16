<template>
    <section class="section section-components">
        <div class="container">
            <h2 class="mt-lg mb-5">
                <span>Detection List</span>
            </h2>            

            <table class="table">
              <thead>
                  <tr>
                      <th class="text-center">#</th>
                      <th>Picture</th>
                      <th>Time</th>
                      <th>Description</th>
                      <th class="text-right">Actions</th>
                  </tr>
              </thead>
              <tbody>
                  <tr>
                      <td class="text-center">1</td>
                      <td><img v-lazy="'img/strangers/Pict.1.png'" alt="Raised image" class="img-fluid rounded shadow-lg" style="width: 150px;"></td>
                      <td>2021-11-02 07:40:01</td>
                      <td>Stranger</td>
                      <td class="td-actions text-right">
                        <button type="button" rel="tooltip" class="btn btn-info btn-icon btn-sm " data-original-title="" title="" @click="modals.modal1 = true">
                          <i class="ni ni-badge pt-1"></i>
                        </button>
                        <modal :show.sync="modals.modal1">
                            <h6 slot="header" class="modal-title" id="modal-title-default"></h6>
                            <img v-lazy="'img/strangers/Pict.1.png'" alt="Raised image" class="img-fluid rounded shadow-lg" style="width: 500px;">
                        </modal>
                      </td>
                  </tr>
                  <tr>
                      <td class="text-center">2</td>
                      <td><img v-lazy="'img/strangers/Pict.2.png'" alt="Raised image" class="img-fluid rounded shadow-lg" style="width: 150px;"></td>
                      <td>2021-11-02 07:40:01</td>
                      <td>Stranger</td>
                      <td class="td-actions text-right">
                        <button type="button" rel="tooltip" class="btn btn-info btn-icon btn-sm " data-original-title="" title="" @click="modals.modal2 = true">
                          <i class="ni ni-badge pt-1"></i>
                        </button>
                        <modal :show.sync="modals.modal2">
                            <h6 slot="header" class="modal-title" id="modal-title-default"></h6>
                            <img v-lazy="'img/strangers/Pict.2.png'" alt="Raised image" class="img-fluid rounded shadow-lg" style="width: 500px;">
                        </modal>
                      </td>
                  </tr>
                  <tr>
                      <td class="text-center">3</td>
                      <td><img v-lazy="'img/strangers/Pict.3.png'" alt="Raised image" class="img-fluid rounded shadow-lg" style="width: 150px;"></td>
                      <td>2021-11-02 07:40:01</td>
                      <td>Stranger</td>
                      <td class="td-actions text-right">
                        <button type="button" rel="tooltip" class="btn btn-info btn-icon btn-sm " data-original-title="" title="" @click="modals.modal3 = true">
                          <i class="ni ni-badge pt-1"></i>
                        </button>
                        <modal :show.sync="modals.modal3">
                            <h6 slot="header" class="modal-title" id="modal-title-default"></h6>
                            <img v-lazy="'img/strangers/Pict.3.png'" alt="Raised image" class="img-fluid rounded shadow-lg" style="width: 500px;">
                        </modal>
                      </td>
                  </tr>
              </tbody>
          </table>

        </div>
    </section>
</template>
<script>
import Modal from "@/components/Modal.vue";
export default {
  components: {
    Modal
  },
  data() {
    return {
      modals: {
        modal1: false,
        modal2: false,
        modal3: false
      }
    };
  }
};
</script>
<style>
</style>

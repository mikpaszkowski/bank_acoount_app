<template>
  <div>
    <div class="container container-lower">
      <div class="module">
        <div class="nav">
          <div class="headline">Email & Phone</div>
          <div class="edit-button-svg">
            <ion-icon
              name="create-outline"
              id="edit-icon"
              @click="toggleModal"
            ></ion-icon>
          </div>
        </div>

        <div class="labels">
          <div class="info">
            <div class="info-name">
              <div class="primary"></div>
              <p>Email:</p>
            </div>
            <div class="info-data">
              <p id="email_p">
                {{
                  currentEmailAddressCom.length > 0
                    ? currentEmailAddressCom
                    : currentEmailAddress
                }}
              </p>
            </div>
          </div>

          <div class="info">
            <div class="info-name">
              <div class="primary"></div>
              <p>Email:</p>
            </div>
            <div class="info-data">
              <p id="email_p">
                {{
                  additionalEmailAddressCom.length > 0
                    ? additionalEmailAddressCom
                    : additionalEmailAddress
                }}
              </p>
            </div>
          </div>

          <div class="info">
            <div class="info-name">
              <div class="primary"></div>
              <p>Phone:</p>
            </div>
            <div class="info-data">
              <p>
                {{
                  currentPhoneNumberCom.length > 0
                    ? currentPhoneNumberCom
                    : phoneNumber
                }}
              </p>
            </div>
          </div>

          <div class="info">
            <div class="info-name">
              <div class="primary"></div>
              <p>Phone:</p>
            </div>
            <div class="info-data">
              <p>
                {{
                  additionalPhoneNumberCom.length > 0
                    ? additionalPhoneNumberCom
                    : additionalPhoneNumber
                }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <transition name="slide-fade">
      <ModalEmailAddress class="modal" v-if="modalOpened" @close="closeModal" />
    </transition>
  </div>
</template>

<script>
import ModalEmailAddress from "./UserProfileDetailsEmailPhoneEdit.vue";
import { mapGetters } from "vuex";

export default {
  components: { ModalEmailAddress },

  data() {
    return {
      modalEmailAddress_open: false,
      phoneNumber: "",
      currentEmailAddress: "",
      additionalPhoneNumber: "",
      additionalEmailAddress: "",
      modalOpened: false,
    };
  },
  methods: {
    toggleModal: function () {
      this.modalOpened = !this.modalOpened;
      if (this.modalOpened) {
        this.scrollToElement();
      }
    },
    scrollToElement() {
      setTimeout(() => {
        let element = document.querySelector(".modal");
        if (element) {
          element.scrollIntoView({ behavior: "smooth", block: "center" });
        }
      }, 100);
    },
    closeModal: function () {
      this.modalOpened = false;
    },
    ...mapGetters("user", [
      "getCurrentPhoneNumber",
      "getCurrentEmailAddress",
      "getAdditionalEmailAddress",
      "getAdditionalPhoneNumber",
    ]),
  },
  computed: {
    ...mapGetters("user", {
      currentPhoneNumberCom: "getCurrentPhoneNumber",
      currentEmailAddressCom: "getCurrentEmailAddress",
      additionalEmailAddressCom: "getAdditionalEmailAddress",
      additionalPhoneNumberCom: "getAdditionalPhoneNumber",
    }),
  },
  mounted() {
    this.phoneNumber = this.getCurrentPhoneNumber;
    this.currentEmailAddress = this.getCurrentEmailAddress;
    this.additionalPhoneNumber = this.getAdditionalPhoneNumber;
    this.additionalEmailAddress = this.getAdditionalEmalAddress;
  },
};
</script>




<style lang="scss" scoped>
@import "../styles/main.scss";
</style>
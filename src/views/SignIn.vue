<template>
  <div class="container top-0 position-sticky z-index-sticky">
    <div class="row">
      <div class="col-12">
        <navbar
          is-blur="blur blur-rounded my-3 py-2 start-0 end-0 mx-4 shadow"
          btn-background="bg-gradient-success"
          :dark-mode="true"
        />
      </div>
    </div>
  </div>
  <main class="mt-0 main-content main-content-bg">
    <section>
      <div class="page-header min-vh-75">
        <div class="container">
          <div class="row">
            <div class="mx-auto col-xl-4 col-lg-5 col-md-6 d-flex flex-column">
              <div class="mt-8 card card-plain">
                <div class="pb-0 card-header text-start">
                  <h3 class="font-weight-bolder text-success text-gradient">
                    Chào mừng bạn đã quay lại!
                  </h3>
                  <p class="mb-0">Đăng nhập</p>
                </div>
                <div class="card-body">
                  <div class="text-start">
                    <label>Email</label>
                    <soft-input
                      id="email"
                      type="email"
                      placeholder="Email"
                      name="email"
                    />
                    <label>Mật khẩu</label>
                    <soft-input
                      id="password"
                      type="password"
                      placeholder="Mật khẩu"
                      name="password"
                    />
                    <soft-switch id="rememberMe" name="rememberMe" checked>
                      Nhớ tài khoản đăng nhập
                    </soft-switch>
                    <div class="text-center">
                      <soft-button
                        class="my-4 mb-2"
                        variant="gradient"
                        color="success"
                        full-width
                        @click="login"
                        >Đăng nhập
                      </soft-button>
                    </div>
                  </div>
                </div>
                <div class="px-1 pt-0 text-center card-footer px-lg-2">
                  <p class="mx-auto mb-4 text-sm">
                    Không có tài khoản?
                    <router-link
                      :to="{ name: 'Sign Up' }"
                      class="text-success text-gradient font-weight-bold"
                      >Đăng ký</router-link
                    >
                  </p>
                </div>
              </div>
            </div>
            <div class="col-md-6">
              <div
                class="top-0 oblique position-absolute h-100 d-md-block d-none me-n8"
              >
                <div
                  class="bg-cover oblique-image position-absolute fixed-top ms-auto h-100 z-index-0 ms-n6"
                  :style="{
                    backgroundImage:
                      'url(' +
                      require('@/assets/img/curved-images/curved9.jpg') +
                      ')',
                  }"
                ></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
  <app-footer />
</template>

<script>
import Navbar from "@/examples/PageLayout/Navbar.vue";
import AppFooter from "@/examples/PageLayout/Footer.vue";
import SoftInput from "@/components/SoftInput.vue";
import SoftSwitch from "@/components/SoftSwitch.vue";
import SoftButton from "@/components/SoftButton.vue";
const body = document.getElementsByTagName("body")[0];
import { mapMutations } from "vuex";
import axios from "axios";
import { message } from 'ant-design-vue';


export default {
  name: "SignIn",
  components: {
    Navbar,
    AppFooter,
    SoftInput,
    SoftSwitch,
    SoftButton,
  },
  created() {
    this.toggleEveryDisplay();
    this.toggleHideConfig();
    body.classList.remove("bg-gray-100");
  },
  beforeUnmount() {
    this.toggleEveryDisplay();
    this.toggleHideConfig();
    body.classList.add("bg-gray-100");
  },
  methods: {
    ...mapMutations(["toggleEveryDisplay", "toggleHideConfig"]),
    async login() {
      try {
        const response = await axios.post(
          "http://localhost:8082/api/user/login",
          {
            "loginName": "admin",
            "password": "123456"
          },
        );
        console.log({response});
        this.success();
        this.$router.push('/tables');
      } catch (error) {
        console.log(error);
      }
    },
    success : () => {
      message.success({
        content: () => 'Đăng nhập thành công',
        class: 'custom-class',
        style: {
          marginTop: '15vh',
        },
      });
    }
  },
};
</script>

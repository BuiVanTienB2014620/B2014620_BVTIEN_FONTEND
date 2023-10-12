
 <template>
    <div v-if="contact" class="page">
      <h4>Hiệu chỉnh liên hệ</h4>
      <ContactForm
        :contact="contact"
        @submit:contact="updatecontact"
        @delete:contact="deletecontact"
      />
      <p>{{ message }}</p>
    </div>
  </template>
  
  <script>
  import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service.js";
  
  export default {
    components: {
      ContactForm,
    },
    props: {
      id: { type: String, require: true },
    },
    data() {
      return {
        contact: null,
        message: "",
      };
    },
    methods: {
      async getContact(id) {
        try {
          this.contact = await ContactService.get(id);
        } catch (error) {
          // chuyển sang trang NotFound đồng thời giữ cho URL không đổi
          this.$router.push({
            name: "NotFound",
            params: {
              pathMatch: this.$route.path.split("/").slice(1),
            },
            query: this.$route.query,
            hash: this.$route.hash,
          });
        }
      },
      async updatecontact(data) {
        try {
          await ContactService.update(this.contact._id, data);
          this.message = "Cập nhật liên hệ thành công";
        } catch (error) {
          console.log(error);
        }
      },
      async deletecontact() {
        if (confirm("Bạn có muốn xóa liên hệ này!")) {
          try {
            await ContactService.delete(this.contact._id);
            this.$router.push({ name: "contactbook" });
          } catch (error) {
            console.log(error);
          }
        }
      },
    },
    created() {
      this.getContact(this.id);
      this.message = "";
    },
  };
  </script>

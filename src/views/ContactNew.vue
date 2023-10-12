
<template>
<div class="page">
  <h4>Thêm mới liên hệ</h4>
  <ContactFormNew @submit:contact="createContact" />
</div>
<p>{{ message }}</p>
</template>

<script>
import ContactFormNew from "@/components/ContactFormNew.vue";
import ContactService from "@/services/contact.service.js";

export default {
  components: {
    ContactFormNew,
  },
  props: {
    contact: { type: Object, require: true },
  },
  
  data() {
    return {
     
      message: "",
    };
  },
  methods: {
    
    async createContact(data) {
      // Hiển thị cửa sổ xác nhận
      const confirmed = window.confirm("Bạn có thêm liên hệ mới?");

      if (confirmed) {
        try {
          await ContactService.create(data);
          this.message = "Thêm liên hệ thành công";
        } catch (error) {
          console.log(error);
        }
      }
    },
  },
};
</script>

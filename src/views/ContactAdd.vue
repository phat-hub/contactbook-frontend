<template>
    <div class="page">
        <h4>Thêm mới Liên hệ</h4>
        <ContactForm 
            :contact="newContact" 
            @submit:contact="addContact" 
        />
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            newContact: { // Khởi tạo đối tượng liên hệ mới
                name: "",
                email: "",
                address: "",
                phone: "",
                favorite: false,
            },
            message: "",
        };
    },
    methods: {
        async addContact(contactData) {
            try {
                await ContactService.create(contactData); 
                alert("Liên hệ được thêm thành công.");
                this.$router.push({ name: "contactbook" }); 
            } catch (error) {
                console.log(error);
            }
        },
    },
};
</script>

<style scoped>
@import "@/assets/form.css";
</style>

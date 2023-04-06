<template>
    <Form @submit="submitUser" :validation-schema="userFormSchema">
        <div class="form-group">
            <h1 class="text-center font-weight-bold text-primary">ĐĂNG NHẬP</h1>
            <label for="username">Tên Đăng Nhập</label>
            <Field name="username" type="text" class="form-control" v-model="userLocal.username" />
            <ErrorMessage name="username" class="error-feedback" />
        </div>
        <div class="form-group">
            <label for="password">Mật Khẩu</label>
            <Field name="password" type="password" class="form-control" v-model="userLocal.password" />
            <ErrorMessage name="password" class="error-feedback" />
        </div>
        <div class="form-group">
            <button class="btn btn-primary">Đăng Nhập</button>
        </div>
    </Form>
</template>
<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage } from "vee-validate";
export default {
    components: {
        Form,
        Field,
        ErrorMessage,
    },
    emits: ["submit:user"],
    props: {
        user: { type: Object, required: true }
    },
    data() {
        const userFormSchema = yup.object().shape({
            username: yup
                .string()
                .required("Tên phải có giá trị.")
                // .min(2, "Tên phải ít nhất 2 ký tự.")
                .max(50, "Tên có nhiều nhất 50 ký tự."),
            password: yup
                .string()
                .required("MMật khẩu phải có giá trị.")
                .max(50, "E-mail tối đa 50 ký tự."),
        });
        return {
            userLocal: this.user,
            userFormSchema,
        };
    },
    methods: {
        submituser() {
            this.$emit("submit:user", this.userLocal);
        }
    },
};
</script>
<style scoped>
@import "@/assets/form.css";
</style>

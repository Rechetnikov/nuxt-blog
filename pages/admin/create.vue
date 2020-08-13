<template>
  <div class="page-wrap">
    <el-form
      class="w600"
      :model="controls"
      :rules="rules"
      ref="form"
      @submit.native.prevent="onSubmit"
    >
      <h2 class="mb">Добавление нового поста</h2>

      <el-form-item label="Заголовок поста" prop="title">
        <el-input v-model.trim="controls.title" resize="none" :rows="10" />
      </el-form-item>

      <el-form-item label="Текст в формате .md или .html" prop="text">
        <el-input type="textarea" v-model.trim="controls.text" resize="none" :rows="10" />
      </el-form-item>

      <el-dialog title="Предпромотр" :visible.sync="previewDialog">{{ controls.text }}</el-dialog>

      <el-form-item>
        <el-button type="success" plain @click="previewDialog=true" round>Предпросмотр</el-button>
        <el-button type="primary" native-type="submit" round :loading="loading">Создать</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  layout: "admin",
  middleware: ["admin-auth"],
  data() {
    return {
      previewDialog: false,
      loading: false,
      controls: {
        title: "",
        text: "",
      },
      rules: {
        text: [
          {
            required: true,
            message: "Текст не должен быть пустым!",
            trigger: "blur",
          },
        ],
        title: [
          {
            required: true,
            message: "Заголовок не должен быть пустым!",
            trigger: "blur",
          },
        ],
      },
    };
  },
  methods: {
    onSubmit() {
      this.$refs.form.validate(async (valid) => {
        if (valid) {
          this.loading = true;

          const formData = {
            title: this.controls.title,
            text: this.controls.text,
          };

          try {
            await this.$store.dispatch("post/create", formData);
            this.$message.success("Пост создан.");
            this.controls.title = "";
            this.controls.text = "";
          } catch (a) {
          } finally {
            this.loading = false;
          }
        }
      });
    },
  },
};
</script>

<style>
.w600 {
  width: 600px;
}
</style>
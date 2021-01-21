<template>
  <div>
    <a-button type="primary" @click.self="showModal">
      Open Modal
    </a-button>
    <a-modal v-model:visible="visible" title="Title" @ok="handleOk">
      <template #footer>
        <a-button key="back" @click="handleCancel"> Return </a-button>
        <a-button
          key="submit"
          type="primary"
          :loading="loading"
          @click="handleOk"
        >
          Submit
        </a-button>
      </template>
      <a-form
        ref="ruleForm"
        layout="inline"
        :model="formInline"
        :rules="rules"
        @submit="handleAdd"
      >
        <a-form-item name="name">
          <a-input v-model:value="formInline.name" placeholder="Name">
            <template #prefix
              ><UserOutlined style="color: rgba(0, 0, 0, 0.25)"
            /></template>
          </a-input>
        </a-form-item>
        <a-form-item>
          <a-input v-model:value.number="formInline.age" placeholder="Age" />
        </a-form-item>
        <a-form-item>
          <a-button
            type="primary"
            html-type="submit"
            :disabled="formInline.name === '' || formInline.age === ''"
          >
            Log in
          </a-button>
        </a-form-item>
      </a-form>
      <p v-for="(item, index) in list" :key="index">
        name:{{ item.name }}--- age:{{ item.age }}
      </p>
    </a-modal>
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, Ref, ref } from "vue";
import { UserOutlined } from "@ant-design/icons-vue";
export default defineComponent({
  components: {
    UserOutlined,
  },
  setup() {
    const list = ref([
      { name: "name1", age: 16 },
      { name: "name2", age: 17 },
      { name: "name3", age: 18 },
      { name: "name4", age: 19 },
    ]);
    const visible = ref(false);
    const loading = ref(false);
    const showModal = () => {
      visible.value = true;
    };
    const handleOk = () => {
      loading.value = true;
      setTimeout(() => {
        visible.value = false;
        loading.value = false;
      }, 3000);
    };
    const handleCancel = () => {
      visible.value = false;
    };
    const formInline = reactive({
      name: "",
      age: 0,
    });
    const rules = reactive({
      name: [
        {
          required: true,
          message: "Please input Activity name",
          trigger: "blur",
        },
        { min: 3, max: 5, message: "Length should be 3 to 5", trigger: "blur" },
      ],
    });
    const ruleForm: Ref = ref(null);
    const handleAdd = () => {
      ruleForm.value
        .validate()
        .then(() => {
          list.value.push({ name: formInline.name, age: formInline.age });
        })
        .catch((error: any) => {
          if(error.errorFields.length === 0){
            list.value.push({ name: formInline.name, age: formInline.age });
          }
        });
    };
    return {
      list,
      formInline,
      visible,
      loading,
      showModal,
      handleOk,
      handleCancel,
      handleAdd,
      rules,
      ruleForm,
    };
  },
});
</script>

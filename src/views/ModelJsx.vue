<script lang="tsx">
import { defineComponent, reactive, ref, withModifiers } from "vue";
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
    const handleAdd = () => {
      list.value.push({ name: formInline.name, age: formInline.age });
    };
    const formSlots = {
      footer: () => (
        <>
          <a-button key="back" onClick={handleCancel}> Return </a-button>
          <a-button
            key="submit"
            type="primary"
            loading={loading.value}
            onClick={handleOk}
          >
            Submit
          </a-button>
        </>
      )
    }
    const inputSlots = {
      prefix: () => <UserOutlined style="color: rgba(0, 0, 0, 0.25)"/>
    }
    return () => {
      return (
        <div>
          <a-button type="primary" onClick={withModifiers(showModal,['self'])}>
            Open Modal with customized footer
          </a-button>
          <a-modal vModel={[visible.value, 'visible']} title="Title" onOk={handleOk} vSlots={formSlots}>
            {/*注释 */}
            <a-form layout="inline" model={formInline} onSubmit={handleAdd}>
              <a-form-item>
                <a-input vModel={[formInline.name, 'value', ['trim']]} placeholder="Name" vSlots={inputSlots}>
                </a-input>
              </a-form-item>
              <a-form-item>
                <a-input vModel={[formInline.age, 'value', ['number']]} placeholder="Age"/>
              </a-form-item>
              <a-form-item>
                <a-button
                  type="primary"
                  html-type="submit"
                  disabled={formInline.name === '' || formInline.age === 0}
                >
                  Log in
                </a-button>
              </a-form-item>
            </a-form>
            {list.value.map((item,index) => <p key={index}>name:{item.name}--- age:{item.age}</p>)}
          </a-modal>
        </div>
      )
    }
  },
});
</script>
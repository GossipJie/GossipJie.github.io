# 弹框
### 父组件

```
import Vue, { CreateElement } from 'vue'
import { Component, Watch } from 'vue-property-decorator'

import ChildComponent from './add-box.component'

@Component
export default class ParentComponent extends Vue {
  render(h: CreateElement) {
    return (
        <i-button on-click={this.open}>打开弹窗</i-button>
    )
  }
  /**
   * 动态实例化添加组件
   */
  open() {
    /**
     * 实例化组件
     */
    let component = new DynamicComponent().$mount()
    /**
     * 将组件添加到body
     */
    document.body.appendChild(component.$el)
    /**
     * 给组件实例传递prop参数
     */
    component.$props.title = '这是传入的标题'
    /**
     * 监听组件实例的自定义事件
     */
    component.$on('ok', (name: string) => {
      this.$Modal.info({
        content: `您输入了“${name}”`
      })
    })
  }

```

### 子组件

```
import Vue, { CreateElement } from 'vue'
import { Component, Prop, Watch } from 'vue-property-decorator'

@Component
export default class ChildComponent extends Vue {

  render(h: CreateElement) {
    return (
      <modal
        value={this.visible}
        title={this.title}
        mask-closable={false}
        on-on-hidden={this.close}
      >
        <i-input type="text" value={this.name} on-input={(val: string) => this.name = val} />
        <div slot="footer">
          <i-button type="text" on-click={this.cancel}>取消</i-button>
          <i-button type="primary" on-click={this.ok}>确定</i-button>
        </div>
      </modal>
    )
  }

  @Prop()
  title: string

  visible: boolean = false

  name: string = ''

  /**
   * 等待对话框隐藏之后，再执行销毁
   */
  close() {
    /**
     * 销毁组件实例
     */
    this.$destroy()
    /**
     * 移除组件DOM
     */
    this.$el.parentNode.removeChild(this.$el)
  }
  //隐藏弹框
  cancel() {
    this.visible = false
  }
  //点击确定按钮就会触发
  ok() {
    if (!this.name) {
      return this.$Modal.warning({
        content: '请将内容填写完整'
      })
    }
    /**
     * 将执行结果以事件的方式通知父组件调用者
     */
    this.$emit('ok', this.name)
    this.cancel()
  }

  mounted() {
    this.visible = true
    this.$nextTick(() => {

	})
  }

}

```
# 表单验证

```
<i-form ref="box" rules={this.ruleInline} model={this.box}>
	<form-item label="娃娃机名称" prop="name" >
		<i-input type="text" value={this.box.name} placeholder='填写名称' on-input={(val: string) => this.box.name = val} />
	</form-item>
	<form-item label="娃娃状态" prop="status">
		<i-select value={this.box.status} placeholder='选择娃娃状态' on-input={(val: string) => { this.box.status = val }} >
			<i-option value='open'>直接上架</i-option>
			<i-option value='close'>添加到仓库</i-option>
		</i-select>
	</form-item>
	<form-item label="选择娃娃机" prop="dollIds">
        <i-select value={this.box.dollIds} placeholder='选择娃娃机' on-input={(val: string[]) => this.handleSelect(val)} multiple>
            {store.doll.dollList.map((item: any) => {
            return <i-option value={item.dollid}>{item.name}</i-option>
            })}
        </i-select>
	</form-item>
</i-form>
<div slot="footer">
	<i-button type="text" on-click={this.cancel}>取消</i-button>
	<i-button type="primary" on-click={() => this.ok('box')}>确定</i-button>
</div>

box: any = {
    name: '',
    status: '',
    dollIds:[]
}
ruleInline: FormRule = {
    phone: [
      { required: true, message: '请输入手机号码', trigger: 'blur' },
      { pattern: /^0?(13|14|15|17|18)[0-9]{9}$/, message: '手机格式不正确', trigger: 'blur' }
    ],
    hours: [
      { required: true,  type: 'number',message: '请输入课时', trigger: 'blur' }
    ],
    shopId: [
      { required: true, message: '请选择门店', trigger: 'change' }
    ],
    cardStartTime: [
      { required: true, message: '请选择购卡日期', trigger: 'change' }
    ],
    cardEndTime: [
      { required: true, message: '请选择到期日期', trigger: 'change' }
    ],
    price: [
      { required: true, type: 'number', message: '请输入客单总价', trigger: 'blur' }
    ]
  }
ok(name: string) {
    (this.$refs[name] as Form).validate((valid: boolean) => {
      if (valid) {
        //如果通过验证
        this.$emit('ok', userInfo)
      } else {
        this.$Modal.warning({
          content: '请将内容填写完整'
        })
      }
    })
  }

```

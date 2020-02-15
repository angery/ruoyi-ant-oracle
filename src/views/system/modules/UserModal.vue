<template>
  <a-modal
    title="操作"
    style="top: 20px;"
    :width="800"
    v-model="visible"
    :confirmLoading="confirmLoading"
    @ok="handleSubmit"
  >
    <a-form :form="form">
      <a-form-item style="display:none">
        <a-input v-decorator="['userId']"/>
        <a-input v-decorator="['userType']"/>
      </a-form-item>
      <a-form-item
        :labelCol="labelCol"
        :wrapperCol="wrapperCol"
        label="用户名"
      >
        <a-input placeholder="用户名" v-decorator="['loginName', {rules: [{ required: true, message: '请输入用户名' },{ min: 1, max: 30, message: '长度在 1 到 30 个字符', trigger: 'blur' }]}]" />
      </a-form-item>

      <a-form-item
        :labelCol="labelCol"
        :wrapperCol="wrapperCol"
        label="昵称"
      >
        <a-input
          v-decorator="[
            'userName',
            {
              rules: [{ required: true, message: '请输入昵称' },{ min: 1, max: 30, message: '长度在 1 到 30 个字符', trigger: 'blur' }]
            }
          ]"
          placeholder="起一个名字"/>
      </a-form-item>
      <a-form-item
        :labelCol="labelCol"
        :wrapperCol="wrapperCol"
        label="手机号码"
      >
        <a-input placeholder="手机号码" v-decorator="['phonenumber', {rules: [{ required: true, message: '请输入手机号码',isPhone: true },{ min: 11, max: 11, message: '长度在11个字符', trigger: 'blur' }]}]" />
      </a-form-item>
      <a-form-item
        :labelCol="labelCol"
        :wrapperCol="wrapperCol"
        label="邮箱"
      >
        <a-input placeholder="邮箱" v-decorator="['email', {rules: [{ required: true, message: '请输入邮箱' },{ min: 1, max: 50, message: '长度在 1 到 50 个字符', trigger: 'blur' }]}]" />
      </a-form-item>

      <a-form-item
        :labelCol="labelCol"
        :wrapperCol="wrapperCol"
        label="性别"
      >
        <a-select v-decorator="['sex', {initialValue:'0',rules: [{ required: true, message: '请选择性别' }]}]">
          <a-select-option :value="'0'">男</a-select-option>
          <a-select-option :value="'1'">女</a-select-option>
          <a-select-option :value="'2'">未知</a-select-option>
        </a-select>
      </a-form-item>
      <a-form-item
        :labelCol="labelCol"
        :wrapperCol="wrapperCol"
        label="状态"
      >
        <a-select v-decorator="['status', {initialValue:'0',rules: [{ required: true, message: '请选择状态' }]}]">
          <a-select-option :value="'0'">正常</a-select-option>
          <a-select-option :value="'1'">禁用</a-select-option>
        </a-select>
      </a-form-item>

      <a-form-item
        :labelCol="labelCol"
        :wrapperCol="wrapperCol"
        label="部门"
      >
        <a-tree-select
          v-decorator="['deptId', {rules: [{ required: true, message: '请选择部门' }]}]"
          :dropdownStyle="{ maxHeight: '400px', overflow: 'auto' }"
          :treeData="deptTree"
          @change="onChange"
          placeholder="部门"
          treeDefaultExpandAll
        >
        </a-tree-select>
      </a-form-item>

      <a-form-item
        :labelCol="labelCol"
        :wrapperCol="wrapperCol"
        label="描述"
      >
        <a-textarea :rows="5" placeholder="..." v-decorator="['remark', {rules: [{ required: false, message: '请输入描述' },{ min: 0, max: 500, message: '长度在 1 到 500 个字符', trigger: 'blur' }]}]"/>
      </a-form-item>

      <a-form-item
        :labelCol="labelCol"
        :wrapperCol="wrapperCol"
        label="拥有角色"
        hasFeedback
      >
        <a-select
          style="width: 100%"
          mode="multiple"
          v-decorator="['roleIds', {rules: [{ required: true, message: '请选择角色' }]}]"
          :allowClear="true"
        >
          <a-select-option v-for="(action) in roleAll" :key="action.roleId" >{{ action.roleName }}</a-select-option>
        </a-select>
      </a-form-item>

    </a-form>
  </a-modal>
</template>
<script>
import { getRoleAll, saveUser } from '@/api/system'
import pick from 'lodash.pick'
export default {
  name: 'UserModal',
  props: {
    deptTree: {
      type: Array,
      required: true
    }
  },
  components: {
  },
  data () {
    return {
      description: '列表使用场景：后台管理中的权限管理以及角色管理，可用于基于 RBAC 设计的角色权限控制，颗粒度细到每一个操作类型。',
      visible: false,
      labelCol: {
        xs: { span: 24 },
        sm: { span: 5 }
      },
      wrapperCol: {
        xs: { span: 24 },
        sm: { span: 16 }
      },
      confirmLoading: false,
      roleAll: [],
      mdl: {},
      deptCheck: true,
      form: this.$form.createForm(this)
    }
  },
  beforeCreate () {
  },
  created () {
    this.loadRoleAll()
  },
  methods: {
    add () {
      this.form.resetFields()
      this.edit({ userId: 0, deptId: '' })
    },
    edit (record) {
      this.mdl = Object.assign({}, record)
      this.visible = true
      this.$nextTick(() => {
        this.form.setFieldsValue(pick(this.mdl, 'userId', 'loginName', 'userName', 'status', 'roleIds', 'remark', 'deptId', 'email', 'phonenumber', 'userType'))
        // this.form.setFieldsValue({ ...record })
      })
    },
    onChange (value, label, extra) {
      if (extra.triggerNode.$children.length > 0) {
        this.$message.error('不能选择父节点' + `${label}`)
        this.deptCheck = false
      } else {
        this.deptCheck = true
      }
    },
    loadRoleAll () {
      getRoleAll().then(res => {
        this.roleAll = res.rows
        console.log('roleALl', this.roleAll)
      })
    },
    handleSubmit (e) {
      e.preventDefault()
      if (!this.deptCheck) {
        this.$message.error('不能选择父节点')
        return
      }
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log('Received values of form: ', values)
          this.confirmLoading = true
          saveUser(values).then(res => {
            if (res.code === 0) {
              this.$message.success('保存成功')
              this.$emit('ok')
              this.visible = false
            } else {
              this.$message.warning(res.msg)
            }
          }).catch(() => {
            this.$message.error('系统错误，请稍后再试')
          }).finally(() => {
            this.confirmLoading = false
          })
        }
      })
    }
  },
  watch: {
    /*
      'selectedRows': function (selectedRows) {
        this.needTotalList = this.needTotalList.map(item => {
          return {
            ...item,
            total: selectedRows.reduce( (sum, val) => {
              return sum + val[item.dataIndex]
            }, 0)
          }
        })
      }
      */
  }
}
</script>

<template>
  <Card>
    <Form
      :label-width="150"
      :rules="validateRules"
      class="form"
      ref="userForm">
      <FormItem label="当前密码" prop="password">
        <Input type="password" v-model="user.password"></Input>
      </FormItem>
      <FormItem label="新密码" prop="newPassword">
        <Input type="password" v-model="user.newPassword"></Input>
      </FormItem>
      <FormItem label="确认新密码" prop="passwordCheck">
        <Input type="password" v-model="dependence.passwordCheck"></Input>
      </FormItem>
      <FormItem>
        <Button
          type="primary"
          :loading="dependence.modifyButtonLoading"
          @click="onModifyButtonClick()">
          确认修改
        </Button>
        <Button
          style="margin-left: 10px"
          type="primary"
          @click="onBackButtonClick()">
          返回
        </Button>
      </FormItem>
    </Form>
  </Card>
</template>

<script>
import { Form, FormItem, Input, Button, Card } from 'iview'

import MD5 from 'md5.js'

export default {
  name: 'KfcHeaderPassword',
  components: {
    Form,
    FormItem,
    Input,
    Button,
    Card
  },
  data () {
    const validateOldPass = (rule, value, callback) => {
      value = this.user.password
      if (!value || value.length < 3 || value.length > 50) {
        callback(new Error('请输入正确的密码'))
      }
      callback()
    }
    const validatePass = (rule, value, callback) => {
      value = this.user.newPassword
      if (!value || value.length < 3 || value.length > 50) {
        callback(new Error('请输入正确的密码'))
      }
      callback()
    }
    const validatePassCheck = (rule, value, callback) => {
      value = this.dependence.passwordCheck
      if (value === '') {
        callback(new Error('请输入密码'))
      } else if (value !== this.user.newPassword) {
        callback(new Error('密码不一致请确认'))
      } else {
        callback()
      }
    }
    return {
      dependence: {
        passwordCheck: '',
        modifyButtonLoading: false
      },
      user: {
        id: 2,
        password: '',
        newPassword: ''
      },
      validateRules: {
        password: [{ required: true, validator: validateOldPass, trigger: 'blur' }],
        newPassword: [{ required: true, validator: validatePass, trigger: 'blur' }],
        passwordCheck: [{ required: true, validator: validatePassCheck, trigger: 'blur' }]
      }
    }
  },
  created () {
    this.init()
  },
  methods: {
    init () {
      this.user = JSON.parse(localStorage.getItem('user'))
    },
    // view event
    onModifyButtonClick () {
      let validateResult = this.$refs.userForm.validate()
      validateResult.then(isSuccess => {
        if (!isSuccess) {
          return
        }

        this.dependence.modifyButtonLoading = true
        let newPassword = new MD5().update(this.user.newPassword).digest('hex')
        this.$axios.put(`/usrmgr/users/${this.user.id}?password=${newPassword}`)
          .then(() => {
            this.$router.go(-1)
          })
          .finally(() => {
            this.dependence.modifyButtonLoading = false
          })
      })
    },
    onBackButtonClick () {
      this.$router.go(-1)
    }
  }
}
</script>

<style lang="css" scoped>
.form {
  width: 360px;
}
</style>

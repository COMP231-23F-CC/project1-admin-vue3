<template>
  <el-collapse v-model="activeNames">
    <el-collapse-item name="basicInfo">
      <template #title>
        <span class="text-base font-bold">基本信息</span>
      </template>
      <el-descriptions :column="4">
        <el-descriptions-item label="姓名">
          {{ contact.name }}
        </el-descriptions-item>
        <el-descriptions-item label="客户名称">
          {{ contact.customerName }}
        </el-descriptions-item>
        <el-descriptions-item label="手机">
          {{ contact.mobile }}
        </el-descriptions-item>
        <el-descriptions-item label="座机">
          {{ contact.telephone }}
        </el-descriptions-item>
        <el-descriptions-item label="邮箱">
          {{ contact.email }}
        </el-descriptions-item>
        <el-descriptions-item label="QQ">
          {{ contact.qq }}
        </el-descriptions-item>
        <el-descriptions-item label="微信">
          {{ contact.webchat }}
        </el-descriptions-item>
        <el-descriptions-item label="详细地址">
          {{ contact.address }}
        </el-descriptions-item>
        <el-descriptions-item label="下次联系时间">
          {{ contact.nextTime ? formatDate(contact.nextTime) : '空' }}
        </el-descriptions-item>
        <el-descriptions-item label="性别">
          <dict-tag :type="DICT_TYPE.SYSTEM_USER_SEX" :value="contact.sex" />
        </el-descriptions-item>
        <el-descriptions-item label="备注">
          {{ contact.remark }}
        </el-descriptions-item>
      </el-descriptions>
    </el-collapse-item>
    <el-collapse-item name="systemInfo">
      <template #title>
        <span class="text-base font-bold">系统信息</span>
      </template>
      <el-descriptions :column="2">
        <el-descriptions-item label="负责人">
          {{ gotOwnerUser(contact.ownerUserId) }}
        </el-descriptions-item>
        <el-descriptions-item label="创建人">
          {{ contact.creatorName }}
        </el-descriptions-item>
        <el-descriptions-item label="创建时间">
          {{ contact.createTime ? formatDate(contact.createTime) : '空' }}
        </el-descriptions-item>
        <el-descriptions-item label="更新时间">
          {{ contact.updateTime ? formatDate(contact.updateTime) : '空' }}
        </el-descriptions-item>
      </el-descriptions>
    </el-collapse-item>
  </el-collapse>
</template>
<script setup lang="ts">
// TODO 芋艿：后面在 review 么？
import * as ContactApi from '@/api/crm/contact'
import { DICT_TYPE } from '@/utils/dict'
import { formatDate } from '@/utils/formatTime'
import * as UserApi from '@/api/system/user'
const { contact } = defineProps<{ contact: ContactApi.ContactVO }>()

// 展示的折叠面板
const activeNames = ref(['basicInfo', 'systemInfo'])
const gotOwnerUser = (owerUserId: string) => {
  let ownerName = ''
  if (owerUserId !== null && owerUserId != undefined) {
    owerUserId.split(',').forEach((item: string, index: number) => {
      if (index != 0) {
        ownerName =
          ownerName + ',' + userList.value.find((user: { id: any }) => user.id == item)?.nickname
      } else {
        ownerName = userList.value.find((user: { id: any }) => user.id == item)?.nickname || ''
      }
    })
  }
  return ownerName
}
const userList = ref<UserApi.UserVO[]>([]) // 用户列表
/** 初始化 **/
onMounted(async () => {
  userList.value = await UserApi.getSimpleUserList()
})
</script>
<style scoped lang="scss"></style>

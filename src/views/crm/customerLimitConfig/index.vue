<template>
  <!-- 列表 -->
  <ContentWrap>
    <el-tabs>
      <el-tab-pane label="拥有客户数限制">
        <!-- TODO @wanwan：CustomerLimitConfigList，因为它是列表哈 -->
        <CustomerLimitConfDetails :confType="LimitConfType.CUSTOMER_QUANTITY_LIMIT" />
      </el-tab-pane>
      <el-tab-pane label="锁定客户数限制">
        <CustomerLimitConfDetails :confType="LimitConfType.CUSTOMER_LOCK_LIMIT" />
      </el-tab-pane>
    </el-tabs>
  </ContentWrap>
</template>
<script setup lang="ts">
import CustomerLimitConfDetails from '@/views/crm/customerLimitConfig/CustomerLimitConfDetails.vue'
import { LimitConfType } from '@/views/crm/customerLimitConfig/customerLimitConf'

defineOptions({ name: 'CrmCustomerLimitConfig' })
</script>

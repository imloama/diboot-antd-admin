<template>
  <a-card :bordered="false">
    <div class="table-page-search-wrapper">
      <a-form layout="inline" @submit.native="getList">
        <a-row :gutter="48">
          <a-col :md="6" :sm="24">
            <a-form-item label="用户名">
              <a-input placeholder="用户名" v-model="queryParam.authAccount" />
            </a-form-item>
          </a-col>
          <a-col :md="6" :sm="24">
            <a-form-item label="IP地址">
              <a-input placeholder="IP地址" v-model="queryParam.ipAddress" />
            </a-form-item>
          </a-col>
          <a-col :md="6" :sm="24">
            <a-form-item label="登录方式">
              <a-select placeholder="请选择" default-value="" v-model="queryParam.authType">
                <a-select-option
                  v-for="(authType, index) in more.authTypeKvList"
                  :key="index"
                  :value="authType.v"
                >
                  {{ authType.k }}
                </a-select-option>
              </a-select>
            </a-form-item>
          </a-col>
          <a-col :md="6" :sm="24">
            <span class="table-page-search-submitButtons">
              <a-button
                icon="search"
                type="primary"
                htmlType="submit">查询</a-button>
              <a-button
                icon="redo"
                style="margin-left: 8px"
                @click="reset">重置</a-button>
            </span>
          </a-col>
        </a-row>
      </a-form>
    </div>

    <a-table
      ref="table"
      size="default"
      :columns="columns"
      :dataSource="data"
      :pagination="pagination"
      :loading="loadingData"
      @change="handleTableChange"
      rowKey="id"
    >
      <span slot="roleList" slot-scope="text, record">
        <template v-if="record.roleList">
          <a-tag color="cyan" v-for="(role, index) in record.roleList" :key="index">{{ role.name }}</a-tag>
        </template>
        <template v-else>
          <span>-</span>
        </template>
      </span>

      <span slot="action">
        -
      </span>
    </a-table>
  </a-card>
</template>

<script>
import list from '@/components/diboot/mixins/list'

export default {
  name: 'LoginTraceList',
  data () {
    return {
      baseApi: '/iam/loginTrace',
      getMore: true,
      columns: [
        {
          title: '用户类型',
          dataIndex: 'userType'
        },
        {
          title: '用户ID',
          dataIndex: 'userId'
        },
        {
          title: '用户名',
          dataIndex: 'authAccount'
        },
        {
          title: '登录IP',
          dataIndex: 'ipAddress'
        },
        {
          title: '登录方式',
          dataIndex: 'authTypeLabel'
        },
        {
          title: '登录时间',
          dataIndex: 'createTime'
        },
        {
          title: '操作',
          width: '150px',
          dataIndex: 'action',
          scopedSlots: { customRender: 'action' }
        }
      ]
    }
  },
  methods: {
  },
  components: {
  },
  mixins: [list]
}
</script>

<style lang="less" scoped>
  .table-operator {
    margin-bottom: 18px;
  }
</style>

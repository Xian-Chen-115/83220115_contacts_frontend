<template>
  <!-- 顶部区域 -->
  <div style="margin: 10px 10px; display: flex;">
    <el-input v-model="name" style="width: 20%;" placeholder="输入姓名"></el-input>
    <el-button type="primary" style="margin-left: 5px" @click="handleSearch">搜索</el-button>
    <el-button plain style="margin-left: auto;" @click="showAddDialog">+</el-button>
  </div>

  <!-- 表格区域 -->
  <div style="padding: 10px;">
    <el-table :data="data.arr" border stripe>
      <el-table-column type="selection" />
      <el-table-column prop="id" label="编号" width="55" />
      <el-table-column prop="name" label="姓名" />
      <el-table-column prop="phone" label="手机号码" />
      <el-table-column prop="email" label="邮箱" />
      <el-table-column label="" width="150">
        <template #default="scope">
          <el-button @click="showEditDialog(scope.row)" size="small" type="primary">编辑</el-button>
          <el-popover placement="top" width="160">
            <p>确定删除吗？</p>
            <div style="text-align: right; margin: 0">
              <el-button size="small" text @click="visible = false">取消</el-button>
              <el-button size="small" type="primary" @click="confirmDelete(scope.row.id)">确定</el-button>
            </div>
            <template #reference>
              <el-button @click="visible = true" size="small" type="danger">删除</el-button>
            </template>
          </el-popover>
        </template>
      </el-table-column>
    </el-table>
  </div>

  <div class="example-pagination-block">
    <el-pagination
        v-model:current-page="currentPage"
        :page-size="pageSize"
        :total="total"
        layout="prev, pager, next, sizes"
        :page-sizes="[10, 20, 50, 100]"
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
    />
  </div>

  <!-- 新增/编辑用户弹窗 -->
  <el-dialog :title="isEditing ? '编辑' : '新增'" v-model="dialogFormVisible">
    <el-form :model="formData" label-width="80px">
      <el-form-item label="姓名">
        <el-input v-model="formData.name"></el-input>
      </el-form-item>
      <el-form-item label="手机号码">
        <el-input v-model="formData.phone"></el-input>
      </el-form-item>
      <el-form-item label="邮箱">
        <el-input v-model="formData.email"></el-input>
      </el-form-item>
    </el-form>
    <div slot="footer" class="dialog-footer">
      <el-button @click="dialogFormVisible = false">取消</el-button>
      <el-button type="primary" @click="isEditing ? handleUpdate() : handleAdd()">确定</el-button>
    </div>
  </el-dialog>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import request from "@/utils/request";

const name = ref('');
const currentPage = ref(1);
const pageSize = ref(10);
const total = ref(0);
const data = ref({ arr: [] });
const visible = ref(false);
const dialogFormVisible = ref(false);
const isEditing = ref(false);

// 表单数据
const formData = ref({
  id: null,
  username: '',
  password: '',
  name: '',
  phone: '',
  email: ''
});

const handleSizeChange = (newSize) => {
  pageSize.value = newSize;
  fetchData(); // 更新数据
};

const handleCurrentChange = (newPage) => {
  currentPage.value = newPage;
  fetchData(); // 更新数据
};

// 获取分页数据
const fetchData = async () => {
  try {
    const response = await request.get('/user/selectByPage', {
      params: {
        pageNum: currentPage.value,
        pageSize: pageSize.value,
        username: '',
        name: name.value.trim()
      }
    });
    data.value.arr = response.data.list;
    total.value = response.data.total;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};

// 搜索功能
const handleSearch = () => {
  currentPage.value = 1;
  fetchData();
};

// 显示新增弹窗
const showAddDialog = () => {
  isEditing.value = false;
  formData.value = { id: null, username: '', password: '', name: '', phone: '', email: '' };
  dialogFormVisible.value = true;
};

// 显示编辑弹窗
const showEditDialog = (row) => {
  isEditing.value = true;
  formData.value = { ...row };
  dialogFormVisible.value = true;
};

// 新增用户
const handleAdd = async () => {
  try {
    await request.post('/user/add', formData.value);
    dialogFormVisible.value = false;
    fetchData();
  } catch (error) {
    console.error('Error adding user:', error);
  }
};

// 更新用户
const handleUpdate = async () => {
  try {
    await request.put('/user/update', formData.value);
    dialogFormVisible.value = false;
    fetchData();
  } catch (error) {
    console.error('Error updating user:', error);
  }
};

// 删除用户
const confirmDelete = async (id) => {
  try {
    await request.delete(`/user/delete/${id}`);
    fetchData();
  } catch (error) {
    console.error('Error deleting user:', error);
  }
};

onMounted(fetchData);
</script>

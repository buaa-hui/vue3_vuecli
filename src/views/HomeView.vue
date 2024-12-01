<!-- <template>
  <el-row class="tac">
    <el-col :span="12">
      <h5 class="mb-2">Default colors</h5>
      <el-menu
        default-active="2"
        class="el-menu-vertical-demo"
        @open="handleOpen"
        @close="handleClose"
      >
        <el-sub-menu index="1">
          <template #title>
            <el-icon><location /></el-icon>
            <span>Navigator One</span>
          </template>
          <el-menu-item-group title="Group One">
            <el-menu-item index="1-1">item one</el-menu-item>
            <el-menu-item index="1-2">item two</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="Group Two">
            <el-menu-item index="1-3">item three</el-menu-item>
          </el-menu-item-group>
          <el-sub-menu index="1-4">
            <template #title>item four</template>
            <el-menu-item index="1-4-1">item one</el-menu-item>
          </el-sub-menu>
        </el-sub-menu>
        <el-menu-item index="2">
          <el-icon><icon-menu /></el-icon>
          <span>Navigator Two</span>
        </el-menu-item>
        <el-menu-item index="3" disabled>
          <el-icon><document /></el-icon>
          <span>Navigator Three</span>
        </el-menu-item>
        <el-menu-item index="4">
          <el-icon><setting /></el-icon>
          <span>Navigator Four</span>
        </el-menu-item>
      </el-menu>
    </el-col>
  </el-row>
</template>

<script lang="ts" setup>
import {
  Document,
  Menu as IconMenu,
  Location,
  Setting,
} from '@element-plus/icons-vue'
const handleOpen = (key: string, keyPath: string[]) => {
  console.log(key, keyPath)
}
const handleClose = (key: string, keyPath: string[]) => {
  console.log(key, keyPath)
}
</script> -->


<template>
  <div class="upload-container">
    <!-- 图片上传展示 -->
    <div class="image-upload">
      <el-upload
        class="upload-demo"
        :auto-upload="false"
        :on-change="handleImageChange"
        accept="image/*"
      >
        <el-button>点击上传图片</el-button>
      </el-upload>

      <!-- 展示上传的图片 -->
      <div v-if="imageUrl" class="image-preview">
        <img :src="imageUrl" alt="Uploaded Image" />
      </div>
    </div>

    <!-- 视频上传播放 -->
    <div class="video-upload">
      <el-upload
        class="upload-demo"
        :auto-upload="false"
        :on-change="handleVideoChange"
        accept="video/*"
      >
        <el-button>点击上传视频</el-button>
      </el-upload>

      <!-- 播放上传的视频 -->
      <div v-if="videoUrl" class="video-preview">
        <video :src="videoUrl" controls width="400">
          您的浏览器不支持视频播放。
        </video>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import { ElUpload, ElButton } from 'element-plus';

export default {
  components: {
    ElUpload,
    ElButton
  },
  setup() {
    // 图片预览 URL
    const imageUrl = ref(null);

    // 视频预览 URL
    const videoUrl = ref(null);

    // 处理图片上传
    const handleImageChange = (file) => {
      const reader = new FileReader();
      reader.onload = (e) => {
        imageUrl.value = e.target.result;  // 生成图片预览 URL
      };
      // 使用 file.raw 传递 Blob 类型的文件
      reader.readAsDataURL(file.raw);  // 将文件读取为 Data URL
    };

    // 处理视频上传
    const handleVideoChange = (file) => {
      const reader = new FileReader();
      reader.onload = (e) => {
        videoUrl.value = e.target.result;  // 生成视频预览 URL
      };
      // 使用 file.raw 传递 Blob 类型的文件
      reader.readAsDataURL(file.raw);  // 将文件读取为 Data URL
    };

    return {
      imageUrl,
      videoUrl,
      handleImageChange,
      handleVideoChange
    };
  }
};
</script>

<style scoped>
.upload-container {
  padding: 20px;
}

.image-upload, .video-upload {
  margin-bottom: 20px;
}

.image-preview img, .video-preview video {
  margin-top: 10px;
  max-width: 100%;
  max-height: 300px;
}

.upload-demo {
  display: block;
  margin-bottom: 10px;
}
</style>

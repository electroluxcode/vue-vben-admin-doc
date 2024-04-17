# Upload

文件上传组件

## Usage

```vue
<template>
  <BasicUpload :maxSize="20" :maxNumber="10" @change="handleChange" :api="uploadApi" />
</template>
<script lang="ts">
  import { defineComponent } from 'vue';
  import { BasicUpload } from '/@/components/Upload';
  import { uploadApi } from '/@/api/sys/upload';

  export default defineComponent({
    components: { BasicUpload },
    setup() {
      return {
        uploadApi,
        handleChange: (list: string[]) => {
          createMessage.info(`已上传文件${JSON.stringify(list)}`);
        },
      };
    },
  });
</script>
```

## Config

`.env.development` 和 `.env.production` 配置开发和生产的文件上传地址

```bash
# .env.development

VITE_PROXY=[["/upload","http://localhost:3001/upload"]]

::: tip
v3.0.0开始，作者重构了vite.config.ts，新版本不再支持VITE_PROXY环境变量。
:::

# 如果没有跨域问题，则直接使用真实上传地址
VITE_GLOB_UPLOAD_URL=/upload

# .env.production
VITE_GLOB_UPLOAD_URL=/upload

```

## Props

| 属性              | 类型       | 默认值   | 可选值 | 说明                                     |
| ----------------- | ---------- | -------- | ------ | ---------------------------------------- |
| value             | `string[]` | -        | -      | 已上传的文件列表，支持v-model           |
| showPreviewNumber | `boolean`  | true     | -      | 是否显示预览数量                         |
| emptyHidePreview  | `boolean`  | false    | -      | 没有上传文件时是否隐藏预览               |
| helpText          | `string`   | -        | -      | 帮助文本                                 |
| maxSize           | `number`   | 2        | -      | 单个文件最大体积，单位 M                 |
| maxNumber         | `number`   | Infinity | -      | 最大上传数量，Infinity 则不限制          |
| accept            | `string[]` | -        | -      | 限制上传格式，可使用文件后缀名(点号可选)或MIME字符串。例如 `['.doc,','docx','application/msword','image/*']` |
| multiple          | `boolean`  | -        | -      | 开启多文件上传                           |
| uploadParams      | `any`      | -        | -      | 上传携带的参数                           |
| api               | `Fn`       | -        | -      | 上传接口，为上面配置的接口               |
| resultField | `string` | - | 接口返回的字段，如果接口返回数组，可以不填。支持`x.x.x`格式 |
| previewColumns | `any` | - | - | 预览的表单列信息 BasicColumn[] |  |
| beforePreviewData | `(fileList)=>any[]` | - | - | 对预览的返回值进行处理 |  |

## Events

| 事件   | 回调参数           | 返回值 | 说明                     | 版本 |
| ------ | ------------------ | ------ | ------------------------ | - |
| change | `(fileList)=>void` |        | 文件列表内容改变触发事件 | |
| delete | `(record)=>void`   |        | 在上传列表中删除文件的事件                 | |
| preview-delete | `(url:string)=>void`   |        | 在预览列表中删除文件的事件                 | 2.5.3 |

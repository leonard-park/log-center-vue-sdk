# Log Center Vue SDK

Log Center 的官方 Vue SDK，支援 Vue 3 Composition API 和 TypeScript。

## 🚀 快速開始

### 安裝

```bash
npm install @log-center/vue-sdk
```

### 基本使用

```vue
<template>
  <button @click="handleClick">Click me</button>
</template>

<script setup lang="ts">
import { useLogCenter } from '@log-center/vue-sdk';

const logger = useLogCenter({
  baseUrl: 'http://localhost:3000',
  application: 'my-vue-app',
  environment: 'production',
});

const handleClick = async () => {
  await logger.general('ui', 'Button clicked');
};
</script>
```

## 📋 支援的日誌類型

- **General Log**: 一般應用程式日誌
- **API Log**: API 請求/回應日誌
- **Admin Log**: 管理後台操作日誌
- **Email Log**: 電子郵件發送日誌
- **WhatsApp Log**: WhatsApp 消息發送日誌
- **Push Notification Log**: 推送通知日誌

## 🔧 配置選項

```typescript
interface LogCenterConfig {
  baseUrl: string;           // Log Center API 基礎 URL
  application: string;        // 應用程式名稱
  environment?: string;      // 環境 (local/staging/production)
  version?: string;          // 應用版本
  timeout?: number;          // 請求超時時間 (毫秒)
  enableRetry?: boolean;      // 啟用自動重試
  maxRetries?: number;       // 最大重試次數
  retryDelay?: number;       // 重試延遲 (毫秒)
  debug?: boolean;           // 啟用除錯模式
}
```

## 🎯 Vue 3 Composition API 支援

```vue
<template>
  <div>
    <button @click="logUserAction">Log Action</button>
    <button @click="logApiCall">Make API Call</button>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { useLogCenter } from '@log-center/vue-sdk';

const logger = useLogCenter({
  baseUrl: 'http://localhost:3000',
  application: 'my-vue-app',
});

const logUserAction = async () => {
  try {
    await logger.admin(1, 'UserManagement', 'LOGIN', 1, 'admin');
  } catch (error) {
    console.error('Failed to log action:', error);
  }
};

const logApiCall = async () => {
  await logger.api('OUT', 'api.example.com', 'POST', '192.168.1.100');
};

onMounted(() => {
  logger.general('page', 'Component mounted');
});
</script>
```

## 🔄 響應式設計

```vue
<template>
  <div>
    <input v-model="message" placeholder="Enter message" />
    <button @click="sendLog" :disabled="!message">Send Log</button>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useLogCenter } from '@log-center/vue-sdk';

const logger = useLogCenter(config);
const message = ref('');

const sendLog = async () => {
  if (message.value) {
    await logger.general('user', message.value);
    message.value = '';
  }
};
</script>
```

## 📚 範例

查看 `examples/` 目錄中的完整範例：

- `BasicUsageExample.vue` - 基本使用方式
- `CompositionApiExample.vue` - Composition API 整合

## 🧪 測試

```bash
npm test
```

## 📄 授權

ISC

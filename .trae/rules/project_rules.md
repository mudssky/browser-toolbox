# Chrome扩展项目开发规则

## 项目概述

本项目是一个Chrome浏览器扩展，使用React + TypeScript + TailwindCSS技术栈开发。

## 技术栈规范

### 核心技术

- **前端框架**: React 18+
- **类型系统**: TypeScript (严格模式)
- **样式框架**: TailwindCSS
- **构建工具**: 根据项目配置使用相应构建工具
- **包管理**: 使用项目现有的包管理器

### Chrome扩展特定规范

#### Manifest配置

- 使用Manifest V3规范
- 严格遵循Chrome扩展安全策略
- 合理配置权限，遵循最小权限原则

#### 架构模式

- **Background Script**: 使用Service Worker模式
- **Content Script**: 注意与页面环境隔离
- **Popup/Options**: 使用React组件化开发
- **消息传递**: 使用Chrome Extension API进行组件间通信

## 代码规范

### TypeScript规范

- 启用严格类型检查
- 优先使用接口(interface)定义类型
- 为Chrome Extension API调用添加适当的类型声明
- 避免使用any类型，必要时使用unknown

### React开发规范

- 优先使用函数组件和Hooks
- 遵循React最佳实践和性能优化
- 组件命名使用PascalCase
- 自定义Hook以use开头

### 样式规范

- 优先使用TailwindCSS工具类
- 避免内联样式，除非动态计算
- 响应式设计考虑扩展弹窗的尺寸限制
- 保持设计简洁，符合Chrome扩展UI规范

### 文件组织

```
src/
├── background/     # Background script相关
├── content/        # Content script相关
├── popup/          # 弹窗页面
├── options/        # 选项页面
├── components/     # 共享组件
├── hooks/          # 自定义Hooks
├── utils/          # 工具函数
├── types/          # 类型定义
└── assets/         # 静态资源
```

## 开发约束

### 安全要求

- 严格遵循CSP(Content Security Policy)
- 不使用eval()或类似的动态代码执行
- 敏感数据使用Chrome Storage API安全存储
- 网络请求遵循CORS策略

### 性能要求

- Content Script保持轻量，避免影响页面性能
- 合理使用Chrome Extension API，避免频繁调用
- 图片资源优化，使用SVG或WebP格式
- 代码分割，按需加载

### 兼容性要求

- 支持Chrome 88+版本
- 考虑不同操作系统的兼容性
- 处理API权限被拒绝的情况

## 调试和测试

### 开发调试

- 使用Chrome DevTools调试
- Background Script在Service Worker中调试
- Content Script在页面控制台调试
- 使用chrome://extensions/开发者模式

### 错误处理

- 所有异步操作添加错误处理
- 用户友好的错误提示
- 记录关键错误信息用于调试

## 发布规范

### 版本管理

- 遵循语义化版本控制
- 更新manifest.json中的版本号
- 维护CHANGELOG.md

### 打包发布

- 移除开发依赖和调试代码
- 压缩和优化资源文件
- 验证所有功能在生产环境正常工作

## 注意事项

1. **权限申请**: 只申请必要的权限，避免过度权限申请
2. **用户体验**: 扩展应该增强而不是干扰用户的浏览体验
3. **隐私保护**: 不收集不必要的用户数据
4. **更新兼容**: 考虑扩展更新时的数据迁移和兼容性
5. **国际化**: 如需支持多语言，使用Chrome i18n API

## 推荐工具和库

- **类型定义**: @types/chrome
- **状态管理**: 根据复杂度选择Context API或Zustand
- **工具库**: lodash-es (按需引入)
- **图标**: Lucide React
- **UI组件**: 根据需要选择轻量级组件库

---

遵循以上规则，确保Chrome扩展项目的代码质量、安全性和用户体验。

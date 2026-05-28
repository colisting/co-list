# Co_List 部署指南

## 📁 文件清单
```
Co_List/
├── index.html       ← 主程序
├── manifest.json    ← PWA 配置
├── sw.js            ← 离线缓存
├── icons/
│   ├── icon-192.png
│   └── icon-512.png
└── README.md        ← 本文件
```

---

## 第一步：创建 Firebase 项目（免费）

1. 打开 https://console.firebase.google.com
2. 点击「添加项目」，随便取个名字，关掉 Google Analytics（不需要）
3. 创建完成后，点左边「构建」→「Authentication」
   - 点「开始使用」
   - 启用「电子邮件/密码」登录
   - 启用「Google」登录（点 Google → 填项目支持邮箱 → 保存）
4. 点左边「构建」→「Firestore Database」
   - 点「创建数据库」
   - 选「以测试模式启动」→ 选任意地区 → 完成
5. 点左边「项目概览」旁的齿轮 ⚙ →「项目设置」
   - 往下滚到「您的应用」→ 点「</>」网页图标
   - 应用昵称随便填，点「注册应用」
   - 复制显示的 `firebaseConfig` 里的内容（下一步用）

---

## 第二步：填入配置

打开 `index.html`，找到这段（约第 600 行）：

```javascript
const firebaseConfig = {
  apiKey:            "YOUR_API_KEY",
  authDomain:        "YOUR_PROJECT.firebaseapp.com",
  projectId:         "YOUR_PROJECT_ID",
  storageBucket:     "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId:             "YOUR_APP_ID"
};
```

把每个 `"YOUR_..."` 替换成 Firebase 给你的真实值，保存文件。

---

## 第三步：上传到 GitHub Pages

1. 打开 https://github.com → 登录 → 右上角 `+` → New repository
2. 仓库名随便填（如 `my-colist`），选 **Public**，点「Create repository」
3. 点「uploading an existing file」→ 把 `Co_List` 文件夹里**所有文件和 icons 文件夹**拖进去
4. 滚到底部点「Commit changes」
5. 进入仓库 → 点「Settings」→ 左边「Pages」
   - Source 选「Deploy from a branch」
   - Branch 选「main」，文件夹选「/ (root)」→ 点 Save
6. 等 1~2 分钟，刷新页面，顶部会出现你的网址：
   `https://你的用户名.github.io/my-colist`

---

## 第四步：配置 Google 登录授权域名

回到 Firebase 控制台：
1. 「Authentication」→「Settings」→「已获授权的网域」
2. 点「添加网域」→ 填入你的 GitHub Pages 网址（不含 https://）
   例如：`你的用户名.github.io`
3. 保存

---

## 第五步：添加到手机桌面

**iPhone（Safari）：**
1. Safari 打开你的 GitHub Pages 网址
2. 底部点分享按钮 `□↑`
3. 选「添加到主屏幕」→ 点「添加」
4. 桌面出现 Co_List 图标，点开就是全屏 App 体验 ✦

**安卓（Chrome）：**
1. Chrome 打开网址
2. 右上角菜单 `⋮` → 「添加到主屏幕」
3. 或等 Chrome 自动弹出安装提示，点「安装」

---

## 关于数据安全

- 你的数据加密存储在 Firebase（Google 服务器），只有登录你账号才能读取
- GitHub 上只有空白的代码，没有任何个人数据
- Firestore 免费版每天限额：读 50,000 次 / 写 20,000 次，日常使用完全够用

---

## 手机修改代码后如何更新

1. 手机浏览器打开 github.com，进你的仓库
2. 点 `index.html` → 右上角铅笔 ✏️ 编辑
3. 修改完 → 滚到底部 → 「Commit changes」
4. 等约 1 分钟，刷新你的网址即可看到新版本

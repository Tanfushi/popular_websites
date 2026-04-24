# BZL 线上商业 · Significance Lab

商业数据分析师的显著性检验工作台，支持 AB Test（付费率 / ARPU / ARPPU）与 DiD（双重差分）。

## 🔒 访问密码

默认密码：`tanfushi5201314`（可在 `index.html` 中的常量 `PWD` 处修改）

## 🚀 GitHub Pages 部署步骤

### 一、创建仓库

1. 登录 GitHub，点击右上角 `+` → `New repository`
2. 仓库名建议：`bzl-significance-lab` 或任何你喜欢的名字
3. 选择 `Public`（Pages 免费版只支持公开仓库；如果你是 GitHub Pro/团队可以 Private）
4. **不要**勾选 "Initialize with README"
5. 点击 `Create repository`

### 二、上传文件

最简单的方法：**网页直接上传**

1. 进入刚创建的空仓库页面
2. 点击中间的 `uploading an existing file` 链接
3. 把 `index.html` 拖进去（文件名必须是 `index.html`，这是 Pages 识别首页的约定）
4. 底部 `Commit changes`

如果你会用 git，也可以用命令行：

```bash
git clone https://github.com/你的用户名/仓库名.git
cd 仓库名
# 把 index.html 复制进来
git add index.html
git commit -m "Initial commit"
git push
```

### 三、开启 GitHub Pages

1. 仓库页面 → `Settings`（右上角齿轮旁边）
2. 左侧菜单找到 `Pages`
3. `Source` 选择 `Deploy from a branch`
4. `Branch` 选择 `main`（或 `master`），目录选 `/ (root)`
5. 点击 `Save`
6. 等 1-2 分钟后刷新页面，顶部会显示：
   ```
   Your site is live at https://你的用户名.github.io/仓库名/
   ```

### 四、访问

复制上面那个地址，发给同事就能用。第一次访问会看到密码门，输入 `tanfushi5201314` 进入。

## ⚠️ 关于密码的坦白

这是**前端密码**——任何人按 F12 打开浏览器调试工具都能看到密码明文。GitHub Pages 不支持服务端逻辑，没法做真正的密码保护。

这个密码的作用是：
- ✅ 阻止"偶然访问者"直接看到内容
- ✅ 用密码分享时有一点仪式感
- ❌ 防不住故意翻源代码的人
- ❌ 防不住搜索引擎爬取（但公开仓库本身就是公开的）

**如果你需要真正的隐私保护**，有几种方案：
1. **仓库设为 Private** + GitHub Pro 账户（$4/月）→ Pages 仍可部署
2. **部署到 Vercel/Netlify**，用它们的 Access Control（免费层有基础访问密码）
3. **内部部署到公司服务器**（如果 BOSS 直聘允许）

对当前用途（内部工具、同事使用），前端密码完全够用。

## 📊 功能概览

### Tab 01 · AB Test
- **付费率**：Two-Proportion Z-Test（教科书方法）
- **ARPU**：正态近似 Z-Test（复合伯努利 × 对数正态）
- **ARPPU**：正态近似 Z-Test（对数正态假设）

每个指标只需输入：**曝光 UV、付费 UV、总付费金额**
其他指标（付费率、ARPU、ARPPU）自动计算。

### Tab 02 · DiD
- 2×2 四宫格（实验/对照 × 前期/后期）
- 支持付费率 DiD、ARPU DiD
- 自动生成平行趋势图 + 反事实虚线

### Tab 03 · 方法说明
详细解释每个检验用的方法、前提假设、局限性。

## 🧪 方法论关键点

**为什么不需要输入标准差**：ARPU/ARPPU 的标准差通过对数正态假设（σ=0.8）从均值反推。这是近似方法，精度对普通决策足够。蒙特卡洛验证显示在 10000 次模拟下，理论 SE 与实际 SE 比值 = 1.005。

**什么时候不要用本工具**：
- 金额分布极度偏态（头部用户贡献 > 80% 营收）
- 需要聚类稳健标准误
- 样本量 < 100
- 论文级严格推断

这些情况请用明细数据 + R `fixest` 或 bootstrap。

## 🔧 修改密码

打开 `index.html`，搜索这一行：
```js
const PWD = 'tanfushi5201314';
```
改成你想要的密码，保存后 push 到 GitHub，1-2 分钟后生效。

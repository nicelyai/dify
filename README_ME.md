# 同步原仓库 Tag 的方法

在 GitHub 上 fork 仓库后，默认情况下**不会自动同步原仓库的标签（tags）**，但你可以通过手动操作同步这些标签。以下是具体步骤：

---

### **同步原仓库 Tag 的方法**
1. **添加原仓库为上游远程（Upstream）**  
   进入你本地克隆的 fork 仓库目录，执行：
   ```bash
   git remote add upstream https://github.com/langgenius/dify.git
   ```

2. **从上游仓库拉取最新的 tags**  
   执行以下命令获取原仓库的所有更新，包括分支和 tags：
   ```bash
   git fetch upstream --tags
   ```

3. **将 tags 推送到你的 GitHub fork**  
   将本地的 tags 同步到你的远程 fork 仓库：
   ```bash
   git push origin --tags
   ```

---

### **选择性拉取指定 tags**
#### **方法 1：使用通配符匹配**
如果 tags 有规律命名（例如 `v1.0.0`, `v2.0.0`），可以用通配符筛选：
```bash
git fetch upstream --tags --no-tags  # 先禁用默认拉取所有 tags
git fetch upstream tag "v1.*"       # 仅拉取 v1.x.x 的 tags
```

#### **方法 2：拉取单个 tag**
```bash
git fetch upstream tag 标签名
# 例如：
git fetch upstream tag v2.3.0
```

#### **方法 3：基于提交信息过滤（高级）**
1. 获取所有 tags 的提交信息：
   ```bash
   git ls-remote --tags upstream
   ```
2. 根据提交哈希或 tag 名称手动拉取需要的 tags。

---


### **推送指定 tags 到你的 GitHub fork**
```bash
# 推送单个 tag
git push origin v2.3.0

# 推送多个 tags（用空格分隔）
git push origin v1.0.0 v1.1.0

# 使用通配符（例如推送所有 v1.x tags）
git push origin refs/tags/v1.*
```

---


### **注意事项**
• **删除原仓库已废弃的 tags（可选）**  
  如果原仓库删除了某些 tags，而你需要完全同步，可以手动删除本地和远程 fork 中对应的 tags：
  ```bash
  # 删除本地 tag
  git tag -d 标签名
  # 删除远程 tag
  git push origin :refs/tags/标签名
  ```

• **强制覆盖（谨慎使用）**  
  如果遇到冲突，可以强制推送 tags（适用于自己的 fork）：
  ```bash
  git push --tags --force
  ```

• **自动同步脚本（可选）**  
  如果你需要频繁同步，可以编写脚本定期执行上述步骤。

---


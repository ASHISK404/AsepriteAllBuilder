# 这是干什么的？
GitHub Actions 的自动化工作流程，为 Windows、Linux、macOS 构建 Aseprite。</br>
通过使用 GitHub 操作，无需手动编译，也不包含恶意软件。</br>
为了遵守 Aseprite 的 EULA，此工作流程不会将二进制文件上传到工件等公共可访问空间。</br>
该版本可以作为草稿在版本中找到（仅对仓库所有者可见）。

# 如何使用
1. 克隆或fork这个仓库
2. 编辑 /.github/workflows/aseprite_build_deploy.yml
3. 查找并编辑 **os** 行并删除您不需要的 os。

        strategy:
            matrix:
                os: [windows-latest, ubuntu-latest, macOS-latest]
4. 保存并提交。
5. 在每次推送到 master 时，工作流将检查新的 Aseprite 版本。
        
# 技术细节
此工作流程遵循 [Aseprite repo](https://github.com/aseprite/aseprite/blob/master/INSTALL.md) 中所述的说明

1. 每天检查 GitHub 上是否有新的 Aseprite 版本（通过与缓存版本进行比较）
2. 如果版本较新，则创建一个草稿版本，其中构建作业可以放置二进制文件。
3. 开始构建
4. 从缓存中获取 Skia，如果不在缓存中，则下载它
5. 使用 CMake 和 Ninja 编译
6. 创建发布的 zip 并上传到第 2 步中的草稿发布

# 构建时间
每个月你有 2000 分钟来自 GitHub 的免费时间。</br>
不同的操作系统花费不同的分钟数，请参阅 [关于 GitHub Actions 的计费](https://help.github.com/en/github/setting-up-and-managing-billing-and-payments-on-github/about-billing-for-github-actions#about-billing-for-github-actions)</br>
因此，为所有三个操作系统构建将花费 130 分钟（20 * 2+10 * 1+8 * 10）</br>
这就是为什么我们建议您修改 **os** 行以只为您需要的操作系统构建。
|操作系统|分钟|分钟乘数
|---|---|---|
|Windows|20|2|
|Ubuntu|10|1|
|macOS|8|10|

# 对其他 Aseprite 构建器的引用
- https://github.com/haxpor/aseprite-macos-buildsh => 允许您在 macOS 上自动构建的脚本
- https://github.com/Insouciant21/action_aseprite => 使用 GitHub Actions，但目前有未优化的二进制文件，这些是公开可用的，这违反了 Aseprite EULA

# 💴支持 Aseprite
继续支持 Aseprite: https://aseprite.org/#buy

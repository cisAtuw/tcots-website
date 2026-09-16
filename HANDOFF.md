# tcots-website 交接说明

给 yiyliu@uw.edu（GitHub: yiyliu-glitch）

## 网站是什么

这是 "The Church of The Seattleites" 的官网，纯静态网站（HTML + JS，没有构建流程，改完文件直接生效）。

## 正式访问地址

**https://tcots-website-cisuw.netlify.app**

## 内容怎么改

所有可编辑内容都在 `data/` 文件夹的 JS 文件里，直接在 GitHub 网页上编辑对应文件、Commit 到 `main` 分支即可，**改完几秒到几十秒内网站会自动更新**（不需要额外操作）。

| 要改什么 | 改哪个文件 |
|---|---|
| UW 秋季迎新活动（日期/时间/地点） | `data/orientation-schedule.js` |
| 其他活动（Lord's Day、福音聚会等） | `data/events.js` |
| 相册/照片说明文字 | `data/gallery.js` |
| 中英文界面文案 | `data/i18n.js` |
| 见证 / 讲道 / 资源等 | `data/testimonies.js` / `sermons.js` / `resources.js` |
| 网站基本信息（名称、联系方式等） | `data/site.js` |

## ⚠️ 关于相册照片（重要）

`data/gallery.js` 里的照片**不是存在这个仓库里的**，而是引用了另一个仓库 `mileszhanghao/christians-in-seattle-uw` 里已经上传好的图片（跨仓库直接读取，src 字段是完整的 `raw.githubusercontent.com` 链接）。

- **改照片说明文字**：直接在 `gallery.js` 里改 `caption` / `caption_zh` 字段即可
- **加新照片**：需要先把图片上传到 `christians-in-seattle-uw` 仓库的 `images/events/` 对应文件夹，再回 `gallery.js` 照现有格式加一条记录（`src` 填完整链接）
- **风险**：如果 `christians-in-seattle-uw` 那个仓库以后被删除、改名，或者图片被移走，这边的照片会全部失效。如果想更省心，可以把图片真正搬到这个仓库自己的 `images/` 文件夹里（需要手动把图片拖到 GitHub 上传页面上传）

## Netlify 部署做了什么

1. 这个仓库原本是从 `sabrinali-linyi/tcots-website` fork 过来的
2. 在 Netlify 新建了一个项目 **`tcots-website-cisuw`**，连接到 `mileszhanghao/tcots-website` 的 `main` 分支
3. 设置了自动部署：**main 分支有新的 commit，Netlify 会自动重新构建发布**，不需要手动点部署
4. 没有配置构建命令（Build command 留空），因为是纯静态站点，不需要编译

### 如果网站突然不更新了怎么排查
最容易出问题的地方是 **GitHub 的 Netlify App 被意外暂停**（之前踩过这个坑）。检查方法：
1. 打开 https://github.com/settings/installations
2. 看 "Netlify" 这一行有没有显示 "Suspended" 标签
3. 如果有，点进去 "Configure" → 拉到底部 "Danger zone" → 点 "Unsuspend"

## 有权限的人
- `mileszhanghao`（owner）
- `yiyliu-glitch`（collaborator，待接受邀请）


## 关于 Guestbook（留言板）功能

Christians in Seattle at UW（学生社团）网站已经移除了 Guestbook 导航入口，因为学生社团不需要这个功能。如果教会网站（这个仓库）想启用留言板，可以参考那边仓库（christians-in-seattle-uw）里现成的实现：`guestbook.html`、`js/guestbook.js`，以及 `data/site.js` 里的 `guestbook` 配置项（Google Form 嵌入链接 + 已发布 Google Sheet 的 CSV 链接）。把这几部分迁移过来、接上自己的 Google Form/Sheet 即可复用。

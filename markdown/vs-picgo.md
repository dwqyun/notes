# vs-picgo 
## 使用 VSCode PicGo 插件 vs-picgo，简单快速搭建 Markdown 专用图床
### 安装配置
1. 在VSCode `Extensions`搜索vs-picgo安装，点击设置图标选择`扩展设置`进入设置项。
2. 具体配置项如下，`current`设置为`github`后，填写`branch`分支(默认为master)，自定义URL`customUrl`填写后可生成图片markdown代码，`path`为仓库下图片存储路径，`repo`为仓库名，`token`在[GitHub](https://github.com/settings/tokens)生成,点击`Generate new toke`勾选repo确认生成后留存备用。
```json
{
   "picgo.picBed.current": "github",
   "picgo.picBed.github.branch": "master",
   "picgo.picBed.github.customUrl": "https://raw.githubusercontent.com/用户名/仓库名/master",
   "picgo.picBed.github.path": "img/",
   "picgo.picBed.github.repo": "用户名/仓库名",
   "picgo.picBed.github.token": "xxx"
}
```
![vs-picgo配置示例图](https://raw.githubusercontent.com/dwqyun/PicBed/master/img/screenshoot20200408214746.png)

### 使用方式
1. 从剪贴板上传快捷键方式，Windows/Unix为`Ctrl + Alt + U`，OsX为`Cmd + Opt + U`。
2. 从资源管理器选择上传快捷键方式，Windows/Unix为`Ctrl + Alt + E`，OsX为`Cmd + Opt + E`。
3. 输入本地资源地址上传快捷键方式，Windows/Unix为`Ctrl + Alt + O`，OsX为`	Cmd + Opt + O`。
4. 以上三种方式上传时，若选中文本则以选中文本为上传文件名。
   
### 注意
- 若无法访问`https://raw.githubusercontent.com`，则需要修改hosts文件，复制hosts文件后添加`199.232.4.133 raw.githubusercontent.com`行，再覆盖到`C:\Windows\System32\drivers\etc`下。
- 可参考[PicGo 配置手册](https://picgo.github.io/PicGo-Doc/zh/guide/config.html#github%E5%9B%BE%E5%BA%8A)
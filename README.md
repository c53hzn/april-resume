## Summary

A resume generator powered by Vite & Vue.

Write your resume like a normal document in yaml format, then get 4 types of layout designs, you can generate static HTML or output as PDF format.

此建立生成器由 Vite 和 Vue 驱动。

只需用 yaml 格式书写简历文档，即可获得 4 种排版设计，你可以选择生成静态 HTML ，或者输出为 PDF 格式。

[Live demo](https://www.houzhenni.com/resume)

## Table of Contents

[How to use](#How-to-use)

[使用说明](#使用说明)

## How to use

This is a resume app that uses Vite and Vue to render data, you can also use browser to print out result as PDF.

First clone this repo to your computer

```
git clone https://github.com/c53hzn/april-cms
```

Then install dependencies

```
npm install
```

Then run script to view demo

```
npm run dev
```

Then go to your browser(Chrome is strongly recommended), go to `localhost:3000`, your resume is ready, you can switch from the 4 layouts and 2 languages, and you can click `print` to export selected resume as PDF format.

If you want to modify the sample resume, go to `resume/` folder, modify the sample resume yaml file, or save as new yaml file and specify the new yaml file name in `src/resume.config.js`, you will be able to view changes immediately.

You can also generate static files and add html file to your website as your resume page.

## 使用说明

此项目是Vite和Vue驱动的简历生成器，可以在浏览器里导出简历为PDF。

先把项目克隆到你的电脑上

```
git clone https://github.com/c53hzn/april-cms
```

然后安装依赖

```
npm install
```

运行脚本开启开发模式

```
npm run dev
```

然后在浏览器（Chrome上可有最佳体验）里打开 `localhost:3000` 即可查看 Demo 简历，APP 中可选 4 款设计，可切换中英文，可点击 `print` 输出 PDF。

如需修改简历内容，可进入`resume/` 文件夹，修改 yaml 文件内容，或者另存为新的 yaml 文件，并在 `src/resume.config.js` 中写明新的简历文件名，刷新页面即可看到新内容。

你也可以生成静态文件，上传到网站上作为自己的简历页。

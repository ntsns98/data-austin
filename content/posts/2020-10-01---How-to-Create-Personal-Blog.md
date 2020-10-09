---
category: Tools
date: 2020-10-01T10:40:32.169Z
description: 介紹如何使用免費開源工具架設個人部落格
draft: false
slug: how-to-create-personal-blog
tags:
  - "Blog"
  - "Gatsby"
  - "Github"
  - "Netlify"
template: post
title: 如何用 Gatsby、Netlify、Github 打造客製化免費部落格
socialImage: "/media/2020-10-01---How-to-Create-Personal-Blog.jpg"
---

- [Abstract](#1-abstract)
- [Workflow](#2-workflow)
- [Environment](#3-environment)
- [CI/CD Your Blog](#4-cicd-your-blog)
- [Epilogue](#5-epilogue)
- [Reference](#6-reference)

# 1. Abstract

這篇的目的是介紹建立 CI/CD 客製化 Blog。適合有 Git 的知識基礎，且想免費建立客製化個人網站，又想和其他人有些區別，可以來參考這條架設部落格的方法，建議稍微有開發經驗的工程師較為適合，因為文章內提到的部分專有名詞我不會著墨太多。不過這個方法不適合所有人，若只是單純想寫文章，建議還是用其他知名免費的 Blog，在 Google search rank 也可以比較高。

# 2. Workflow

![2020-10-01---How-to-Create-Personal-Blog.jpg.jpg](/media/2020-10-01---How-to-Create-Personal-Blog.jpg)

完成後的 CI/CD 流程如圖所示，將新文章更新到 Dev Branch，Netlify 即會產生預覽，每次 Commit 皆會產生一個隨機的亂碼加在 Domain 前面，例如：`https://5f7c35b804a8a50007c68bbb--data-science-austin.netlify.app/`

待 review 沒問題後再部屬到 Production 環境，以本篇為例則會更新到：`https://data-science-austin.netlify.app/`

# 3. Environment


1. 安裝 `Node.js` 
    - 根據 OS，參考官網建議的安裝方式：[Install Node.js for your appropriate operating system]([https://www.gatsbyjs.com/tutorial/part-zero/#install-nodejs-for-your-appropriate-operating-system](https://www.gatsbyjs.com/tutorial/part-zero/#install-nodejs-for-your-appropriate-operating-system))
    - 我的電腦是 Windows，故直接至[官網]([https://nodejs.org/en/](https://nodejs.org/en/))下載最新版即可
2. 安裝 Git
    - 根據 OS，參考官網建議的安裝方式：[Install Git]([https://www.gatsbyjs.com/tutorial/part-zero/#install-git](https://www.gatsbyjs.com/tutorial/part-zero/#install-git))
    - 我的電腦是 Windows，故直接至[官網]([https://gitforwindows.org/](https://gitforwindows.org/))下載最新版即可
3. 安裝 Gatsby CLI

    ```bash
    npm install -g gatsby-cli
    ```

4. 申請 [Github]([https://github.com/](https://github.com/)) 帳號
5. Fork Gatsby starter
    - 為了要能 CI/CD 到 Netlify，需在自己的 Github 有一個 Repository ，故先到[開源的 Gatsby starter]([https://github.com/alxshelepenok/gatsby-starter-lumen](https://github.com/alxshelepenok/gatsby-starter-lumen)) fork master 版本至自己的 Github
    - PS：
        1. 若要在自己的電腦試架本機端服務，可參考 [Quick Start]([https://github.com/alxshelepenok/gatsby-starter-lumen#quick-start](https://github.com/alxshelepenok/gatsby-starter-lumen#quick-start))
        2. 若要使用其他 Starter，可至[官網]([https://www.gatsbyjs.com/starters/](https://www.gatsbyjs.com/starters/))選擇
6. 設定 Netlify
    1. 到[官網]([https://www.netlify.com/](https://www.netlify.com/))辦帳號
    2. Create A New Site 
        - 登入後，點選 `New Site From Git`
        - 選擇 Github
        - 選擇上一個步驟所建立的 Repo
        - Branch to deploy 選擇 Master
        - 按下 Deploy 後會自動部屬
        - 參考：[A Step-by-Step Guide: Gatsby on Netlify]([https://www.netlify.com/blog/2016/02/24/a-step-by-step-guide-gatsby-on-netlify/](https://www.netlify.com/blog/2016/02/24/a-step-by-step-guide-gatsby-on-netlify/))
7. 部屬到這即完成，相關 Netlify 設定可至[官網]([https://docs.netlify.com/configure-builds/get-started/#build-image-selection](https://docs.netlify.com/configure-builds/get-started/#build-image-selection))查看

# 4. CI/CD Your Blog

1. 更新內容

    本篇所使用的 Starter 的結構可參考：[Folder Structure]([https://github.com/alxshelepenok/gatsby-starter-lumen#folder-structure](https://github.com/alxshelepenok/gatsby-starter-lumen#folder-structure))，我有更新過的檔案如下：

    1. `config.js`：基本個人檔案
    2. `content`：Blog 上的內容

    PS： 本人前端不熟，故尚未能提供完整的客製化教學，我只先更新內容而已，待日後學會後再持續更新

2. 在此 Github repository 建立 Brach (建議可下載 [SourceTree]([https://www.sourcetreeapp.com/](https://www.sourcetreeapp.com/))，提供 GUI 的 Git，方便很多)，此目的是 Netlify 提供預覽功能，故可以先 Push 到 brach (ex: dev)，預覽沒問題後再 Pull Request 到 Master
3. 撰寫 Blog
    - 文章位置在 `content/posts`
    - 使用 Markdown 格式
    - 我是用 Pycharm ，因為可在 IDE 提供 Markdown preview
4. 在 Github 安裝 [Netlify App]([https://github.com/apps/netlify](https://github.com/apps/netlify))
5. 設定 Deploy preview: 
    1. 至 Netlify 個人頁面選擇所架設的 Site > Setting > Build & Deploy > Deploy contexts > 選擇 `Production branch`，以及 Deploy previews 選擇 `Any pull request against your production branch / branch deploy branches`，以及 Branch deploys 選擇 `All`
    2. 參考：
        1. [Introducing Deploy Previews in Netlify]([https://www.netlify.com/blog/2016/07/20/introducing-deploy-previews-in-netlify/?_ga=2.228685404.1579865990.1601105370-1463208093.1601105370](https://www.netlify.com/blog/2016/07/20/introducing-deploy-previews-in-netlify/?_ga=2.228685404.1579865990.1601105370-1463208093.1601105370))
        2. [Branch deploy controls]([https://docs.netlify.com/site-deploys/overview/#branch-deploy-controls](https://docs.netlify.com/site-deploys/overview/#branch-deploy-controls))
6. 完成!!! 
    - 每當 Push 時便會自動產生預覽
    - 每當 Push Master 或 Pull request 到 Master，也會更新 Production

# 5. Epilogue

這篇算是一個開始，為之後的文章鋪路，我的 Blog 目的是想建立個人網站(品牌、作品集)、記錄我的學習歷程 (包含工作上的軟、硬實力或是工作外的額外學習)，以及參與比賽的經驗分享，之後也希望能中、英文呈現，順便練習英文表達能力。當初有考慮過 Medium，但沒有 Tag 或 Category 的功能，畫面也不太像是作品集，最後找到網友分享的這篇文章提及的方法。

期許將來能穩定產出些有質量且友善的文章，讓剛踏入這個領域的夥伴能快速上手，內容大部分將會以 Data 相關居多，一來是我本身是 Data engineer，二來我對 Data 的題材比較感興趣。由於我目前工作接下來會將服務上到 AWS，是故打算考個 AWS 相關的證照，預計的 Path：Cloud Practitioner > Developer Associate > Solution Architect Associate > Data Analytics。

# 6. Reference

1. [談再整理自己的文章（下） — 用Gatsby和Netlify建立免費網誌]([https://notes.desktopofsamuel.com/posts/談再整理自己的文章下-用Gatsby和Netlify建立免費網誌](https://notes.desktopofsamuel.com/posts/%E8%AB%87%E5%86%8D%E6%95%B4%E7%90%86%E8%87%AA%E5%B7%B1%E7%9A%84%E6%96%87%E7%AB%A0%E4%B8%8B-%E7%94%A8Gatsby%E5%92%8CNetlify%E5%BB%BA%E7%AB%8B%E5%85%8D%E8%B2%BB%E7%B6%B2%E8%AA%8C))
2. [Gatsby]([https://www.gatsbyjs.com/](https://www.gatsbyjs.com/))
3. [alxshelepenok/gatsby-starter-lumen]([https://github.com/alxshelepenok/gatsby-starter-lumen#folder-structure](https://github.com/alxshelepenok/gatsby-starter-lumen#folder-structure))
4. [Netlify]([https://www.netlify.com/](https://www.netlify.com/))
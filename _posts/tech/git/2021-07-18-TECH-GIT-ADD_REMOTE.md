---
title: Git, Remote repo add
date: 2021-07-18 09:00:00 +0900
categories: [Tech, Git]
tags: [java, tech, git]
---

## 사용 배경
* Git clone해온 원격 저장소말고 다른 저장소와 연결하고 싶을때 사용

## 사용 방법
1. <code>git remote add {저장소_별칭} base_저장소_url</code>
```shell
// 연결하고자하는 git 저장소로 이동

git remote add upstream https://github.com/{...}/{...}.git
```

<br><br>

2. <code>git remote -v</code>
    * 지정한 별칭으로 연결된 저장소가 보이면 연결 완료

<br><br>

3. git fetch {저장소_별칭}
```shell
git fetch upstream [optional]{branch name}
```

<br><br>

4. rebase, merge, push, pull등 upstream과 기존 저장소간 명령어 실행


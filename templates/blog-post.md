<%*
// 제목 입력
const title = await tp.system.prompt("Post Title");

if (!title || title.trim() === "") {
    new Notice("타이틀 비어있음");
    const file = tp.file.find_tfile(tp.file.path(true));
    await app.vault.delete(file);
    return;
}

// 제목 정리
const cleanTitle = title.trim();

// 날짜/시간 생성
const date = tp.date.now("YYYY-MM-DD");
const datetime = tp.date.now("YYYY-MM-DD HH:mm:ss");

// 파일명 생성
const slug = cleanTitle
    .toLowerCase()
    .replace(/[:\[\]{}()'"#?!@$%^&*+=\/\\|<>]/g, '')
    .replace(/\s+/g, '-')
    .replace(/-+/g, '-')
    .replace(/^-|-$/g, '')
    .trim();

if (!slug) {
    new Notice("잘못된 파일명");
    return;
}

const fileName = `${date}-${slug}`;

// 중복 체크
const currentPath = tp.file.path(true);
const folder = currentPath.substring(0, currentPath.lastIndexOf('/'));
const targetPath = `${folder}/${fileName}.md`;
const existingFile = app.vault.getAbstractFileByPath(targetPath);

if (existingFile && existingFile.path !== currentPath) {
    new Notice("파일 중복");
    return;
}

// 파일명 변경
await tp.file.rename(fileName);
new Notice("파일 생성: " + fileName);
-%>
---
title: "<% title %>"
date: <% datetime %> +0900
categories: []
tags: []
comments: true
---

## Overview

---

## References
<%*
// 1. 제목 입력
const title = await tp.system.prompt("Post Title");
if (!title) {
    await tp.file.delete();
    return;
}

// 2. 파일명 생성 (YYYY-MM-DD-slug.md)
const date = tp.date.now("YYYY-MM-DD");
const slug = title
    .toLowerCase()
    .replace(/[^a-z0-9\s-]/g, '')
    .replace(/\s+/g, '-')
    .replace(/-+/g, '-')
    .trim();
const fileName = `${date}-${slug}`;
await tp.file.rename(fileName);

// 3. 카테고리 입력
const categoryInput = await tp.system.prompt("Category (comma separated)");
const categories = categoryInput 
    ? categoryInput.split(',').map(c => c.trim()).join(', ')
    : '';

// 4. 태그 입력
const tagsInput = await tp.system.prompt("Tags (comma separated)");
const tags = tagsInput 
    ? tagsInput.split(',').map(t => t.trim()).join(', ')
    : '';
-%>
---
title: <% title %>
date: <% tp.date.now("YYYY-MM-DD HH:mm:ss") %> +0900
categories: [<% categories %>]
tags: [<% tags %>]
---

## Overview


## Content


## Conclusion



---

## References
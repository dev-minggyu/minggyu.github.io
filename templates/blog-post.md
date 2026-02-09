<%*
// 1. 제목
const title = await tp.system.prompt("Post Title");
if (!title) {
    await tp.file.delete();
    return;
}

// 2. 파일명 생성 및 변경
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
const category = await tp.system.prompt("Category");

// 4. 태그 입력
const tags = await tp.system.prompt("Tags (comma separated)");
-%>
---
title: <% title %>
date: <% tp.date.now("YYYY-MM-DD HH:mm:ss") %> +0900
categories: [<% category %>]
tags: [<% tags %>]
---

# <% title %>

## Overview

<% tp.file.cursor(1) %>

## Content



## Conclusion



---

## References

- 
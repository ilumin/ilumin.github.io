---
title: Set Path Alias for NestJS and Jest
layout: post
date: 2024-07-03
description: Always forgot how to do it
tags: nest, jest
---

## The Problem

NestJS didn't configure path aliases by default. When we create a unit test that might need to import another file, we'll have to import with a weird long path, e.g., `../../services`.

I'm a lazy bastard; I just want to do something easy.

## The Solution

First, add `paths` inside 'compilerOptions' to set the TypeScript path alias at `tsconfig.json`.

```json
{
  "compilerOptions": {
    // ... tsconfig's stuff
    "paths": {
      "@@/*": ["src/*"]
    }
  }
}
```

This configuration means that TS will understand that `import { services } from '@@/services'` is the same as `import { services } from 'src/services'`.

Cool! However, there are still some issues with the test.

Second, let's configure Jest in `package.json` by adding `moduleNameMapper` inside 'jest'.

```json
{
  // ... package.json's stuff
  "jest": {
    // ... jest's stuff
    "rootDir": "src",
    "moduleNameMapper": {
      "@@/(.*)$": "<rootDir>/$1"
    }
  }
}
```

This configuration means that Jest will understand that `import { services } from '@@/services'` is the same as `import { services } from 'src/services'`.

Now, we can use path aliases in NestJS and Jest instead of using a full, weird, long path.
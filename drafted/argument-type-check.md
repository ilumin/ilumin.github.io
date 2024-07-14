---
title: Argument Type Check with TS
layout: post
date: 2024-07-**
description: ทำ type check และ auto suggest ด้วย TS
tags: typescript
---

# ทำ type check และ auto suggest ด้วย TS

```ts
type Route = {
  path: string
}
function router<const T extends Route>(routes: T[]) {
  return {
    navigate(path: T["path"]) {
      // ... implementation
    }
  }
}

const rtr = router([
  {
    path: "/",
  },
  {
    path: "/about",
  }
])

rtr.navigate("/")
rtr.navigate("/about")
rtr.navigate("/faq")
//            ^
// Argument of type "/faq" is not assignable to
// parameter of type "/" | "/about".
```

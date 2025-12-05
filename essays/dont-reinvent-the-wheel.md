---
layout: essay
type: essay
title: "Don't reinvent the wheel"
# All dates must be YYYY-MM-DD format!
date: 2025-12-04
published: true
labels:
  - Design Patterns
---

Throughout the software development process, there are often recurring problems that you may come across. Rather than constantly reimplementing a solution for each problem, you can use reuse design patterns to solve these problems. In addition to optimizing the software development process, design patterns are well-tested approaches that can make your code more readable to you and other developers, as well as easier to maintain. 

In my final project for my software engineering class, I am working with my team members to build a Recipe application using Next.js. With the limited time we have to complete this project before the semester ends, it’s important that we use this time efficiently. Throughout this project we have used a variety of design patterns to aid in implementing different functionalities. One design pattern used in our project is the Singleton Pattern. For example, our database schema defines different models that we use throughout the application. In this case, we do not want to be creating a new instance of a database connection each time we need to use it. Instead, we establish the connection once, then import it into each file in which we need it.

```typescript
// rainbow-recipes/src/lib/prisma.ts
import { PrismaClient } from '@prisma/client';

const globalForPrisma = global as unknown as { prisma: PrismaClient };

// eslint-disable-next-line import/prefer-default-export, operator-linebreak
export const prisma =
  // eslint-disable-next-line operator-linebreak
  globalForPrisma.prisma ||
  new PrismaClient({
    log: ['query'],
  });

if (process.env.NODE_ENV !== 'production') globalForPrisma.prisma = prisma;
```

<img width="200px" class="rounded float-start pe-4" src="../img/wheel/wheel.jpg">

As the saying goes, don’t reinvent the wheel. This is emphasized in software development as reusing code not only saves time, but makes the overall code cleaner and easy to follow.
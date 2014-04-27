---
layout: post
title: "Static, Inline, and Static Inline Explained"
date: 2013-08-29 17:31
comments: true
published: false
tags: ['c++', 'static', 'inline', 'static inline']
---

One C/C++ feature that I hear a lot of confusion about is `static inline`. In order to understand the `static inline` feature, we first have to understand `static` and `inline` individually.

## Static

The first use of the `static` keyword is to declare a static member variable:

    class MyClass {
        static int foo;
    }

    int MyClass::foo = 1

## Inline

## Static Inline

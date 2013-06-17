---
layout: post
title:  "Modification Checklists"
---

When creating a component for the Link, there are often several steps that are often obscure and non-obvious. These checklists
hope create a discrete list of steps for common Link modifications a developer might want to perform.

Adding Support For a New Language
=================================

 - Write the required `bitbake` *recipes* to create binary packages for the language's compiler and libraries.
 - Write the necessary pcompiler *transforms* to compile the language into a binary.
 - Add the language's file extension to botui's *FileActionCompile* class to enable compiling from the Link's embedded file manager.
 - Write a *Lexer* (syntax highlighter) plugin for KISS IDE.
 - Create a *Template Pack* for KISS IDE (File > New > New Template Pack...).
 - Add the required language packages to `meta-kipr/recipes-kovan/images/kovan-kipr-image.bb` to make the language a part of the official firmware.

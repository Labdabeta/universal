# Universal

## Table of Contents

 - [Overview](#overview)
 - [How it works](#how-it-works)

## Overview

Universal is a set of tools for quickly and efficiently creating basic compilers
for new languages. Each aspect of compilation is specified using a unique
programming language specially tailored for its specific task.

This tool is not intended to replace lex, yacc or similar tools. This language
is designed to provide a quick and dirty compiler for many languages to many
other languages. Some uses of this tool include:

 - Testing a new assembly language by loading the C language specification and a
   custom set of compilation rules.
 - Testing a modification to an existing language by loading its specification
   and modifying it.
 - Producing niche compilers which do not need to be optimized (EG: compiling
   golfing languages to scripting languages like Pyth -> Python)

## How it works

These tools allow you to convert language definition files into binary language
compiler files. These compiler files can then by loaded by the universal
compiler to compile appropriate files or else can themselves be compiled to a C
source file which in turn can be compiled into a stand-alone executable.

In order to reduce reliance on each part, the language is first compiled to an
intermediate standardized abstract syntax tree. Then a target language
definition is used to compile that tree into a linear set of instructions.

+++
draft = false
date = "2017-01-09T11:06:05+10:30"
title = "bf.js"
description = ""
tags = ["pointless","javascript","brainfuck"]
categories = ["programming"]

+++

bf.js is a project I made over the course of a few hours of messing around.

I was inspired by pages like JSFiddle which allow people to run snippets of code easily in their browser, however I wanted something that:

1. interpreted a language more interesting and unique than JavaScript and
2. gave more of an insight into what is actually happening behind the scenes.

To that end, I wrote bf.js, a HTML5/JavaScript ES6 based Brainfuck interpreter, which will run a Brainfuck program while showing the state of each memory location between each program step, and when finished will give a simple explanation of the next instruction to be executed and how it will affect the state of the virtual machine.

<img src="/images/bfjs.jpg" width="100%"/>

The bf.js VM has been written as an ES6 class which allows for easy extensability and implementation into a variety of JavaScript environments (browser, NodeJS, etc), although prevents bf.js from being run in older browsers without being passed through something like Browserify.

I have a demo of bf.js available [here](http://nicknelson.io/brainfuck), as well as the code for the project on [GitHub](https://github.com/nicholasnelson/bfjs).
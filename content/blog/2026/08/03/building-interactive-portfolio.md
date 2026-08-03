---
title: Building an interactive portfolio
description: Overview of my experience building a 2D game-like portfolio
date: 2026-08-03
tags: projects
---
About two months ago, I finally got around to building an [interactive portfolio](http://louistsui.ca/portfolio-game) in the style of a 2D game (the code in the [repo](https://github.com/tsuilouis/portfolio-game) was written completely by me). This was inspired by a [FreeCodeCamp post](https://www.freecodecamp.org/news/create-a-developer-portfolio-as-a-2d-game/) I saw back in 2024. In this post I’ll document the “behind the scenes” experience I had while working on the project because some aspects were trickier than I expected, despite the tutorial provided (which was very helpful, don’t get me wrong).

## Foundation
First off, I did not simply fork the original project and replace the dialogue with my own &ndash; I’m more creative than that 😉. What I did was watch JSLegendDev’s [YouTube tutorial](https://www.youtube.com/watch?v=wy_fSStEgMs) in order to understand how he built his portfolio. Topics included the build tool (Vite), the game engine library (Kaboom.js or [Kaplay.js](https://kaplayjs.com); the latter is an active fork of the former), making/acquiring game assets, and the code organization. I paused and replayed segments, following along with my editor and terminal. The most significant deviation I made was during construction of the map. I arranged tiles and defined layers according to my liking. By the end of the tutorial, I had a functional static site, but there were some things that I wanted to tinker with.

## Refining controls
I felt that the controls from the tutorial were a bit janky so I looked into improving them.

### Mouse
There were two issues I observed with the original mouse controls (left mouse button to be exact):
1) When I rapidly clicked the mouse, the player character appeared to be sliding around. The fix I found was to add a `mousepress` handler with the initial animation speed doubled.
2) Supposing I held the mouse down to move the player and trigger some dialogue, if I moved my mouse cursor so that it was on the text window and let go, the player would continue to move nonstop towards my cursor until I clicked (press and release the mouse button) again. The fix I found was to pause the `mousedown` event upon the player colliding with a prop and resume when the user presses the mouse again.

### Keyboard arrow keys
Although the tutorial did not cover how to move with the arrow keys on a keyboard, the [source code](https://github.com/JSLegendDev/2d-portfolio-kaboom) in the repository did. Using that as a reference, I implemented keyboard support for player movement. One notable difference is that the sprite does not animate while multiple keys are held down. I fixed an issue where closing the dialogue with the mouse would cause the arrow keys to stop working because the canvas lost focus.

**Note:** one thing I didn’t figure out yet is how to prevent both mouse and keyboard input from interfering with each other. This causes extra acceleration and odd sprite animation.

## Adding a guide NPC
I wanted to add a non-player character (NPC) to make things more lively. I used an elderly man sprite as my NPC and made him [static](https://kaplayjs.com/docs/api/ctx/body/?preview=BodyCompOpt#BodyCompOpt-isStatic), both for ease of implementation and as a design choice. Having the NPC move would make it more likely for the player to accidentally bump into him and trigger unwanted dialogue.

## Adjusting for mobile experience
I applied a `max-width` and `overflow-x: auto` so that the dialogue would not cover too much of the screen on small viewports.

## Closing thoughts
All in all, this was a pretty fun side project to work on. This was my first real foray with using a game engine, but I did watch some [CS50G](https://cs50.harvard.edu/games/2018) lectures (the archived 2018 version) last year so I had some rudimentary knowledge of game development concepts. An updated version, [CS50 2D](https://cs50.harvard.edu/games), was launched this year (2026) and I hope to complete that course eventually!

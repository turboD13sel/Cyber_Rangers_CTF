Task: The Secret of Java Island is a 2024 point-and-click graphic adventure game developed and published by LA CTF Games. It takes place in a fictional version of Indonesia during the age of hacking. The player assumes the role of Benson Liu, a young man who dreams of becoming a hacker, and explores fictional flags while solving puzzles.
File: game.jar

Solution: First of all I decompiled the game.jar using https://www.decompiler.com/. Got the source code for our game (JavaIsland.java). When we play the game, and we reach the stage where we need to hack the site, we need to enter the sequence or DOM or prototype. As a result, if the combination is correct (A string of 8 characters should be output, for example: "pdddppdd"), then we will get a flag. In the code, this combination is hashed by the SHA256 algorithm in the form of an array of bytes.
Byte array: {69, 70, -81, -117, -10, 109, 15, 29, 19, 113, 61, -123, -39, 82, -11, -34, 104, -98, -111, 9, 43, 35, -19, 22, 52, -55, -124, -45, -72, -23, 96, -77}

I converted it to a user-friendly form: 4546af8bf66d0f1d13713d85d952f5de689e91092b23ed1634c984d3b8e960b3

I wrote python code to hash all possible combinations of "p" and "d" and output the result to notepad (hashing.py).

In the notepad, I found the same hash that I got after converting the byte array into a convenient form and got the correct combination: "dpddpdpp".

Entered this combination in game and got the flag:

# 5. Re:Draw

Her screen went black and a strange command window flickered to life, lines of text flashed across before everything went silent. Moments later, the system crashed. By sheer luck, we recovered a memory dump. Note: There are three stages to this challenge and you will find three flags. What we know: just before the crash, a black command window flickered across the screen, something in its output might still be visible if you dig through memory. She was drawing when it happened, and remnants of a painting program linger, which could reveal more if inspected in the right way. Finally, a mysterious archive hides deeper in memory, likely holding the last piece of her work. Hint: Learn up on volatility 2 and its various plugins and what they are used for.

## Solution:

First i downloaded the rar and extracted it, and got `MemoryDump_Lab1.raw` According to the hint I was supposed to use volatility 2 which i downloaded from github
### Part 1 - using cmd


---
title: 技术笔记
---

# {{ page.title }}


#### how to debug python
```
python -m pdb xxxx.py

```

- n: execute the next line
- p: print the value of an object
- s: step into a function
- r: return from a function
- b [num]: set a breakpoint at line [NUM]
- c: continue to run the code until a break point is met
- unt [NUM]: run the code until line [NUM]
- whatis: print the type of object (similar to p type(some_object))
- l: list the context of current line (default 11 lines)
- h: show help message
- q: quit the debugger

```
breakpoint() //auto break at specified line 
```
#### pycharm cheatsheet

ctrl + shift + i : show definiton, Enter to go there
ctrl + alt + <-  : move cursor to prev pos


#### linux memo

```

sudo netstat -tulpn | grep 80

ps aux | grep ....

```

#### project for colorizing

some collection
https://github.com/MarkMoHR/Awesome-Image-Colorization

CLIP colorizing
https://github.com/luckyhzt/unicolor

Image Hint
https://github.com/KIMGEONUNG/BigColor

facing makeup
https://github.com/VinAIResearch/CPM


color transfer opencv
https://github.com/chia56028/Color-Transfer-between-Images


lasso tool

https://www.losingfight.com/blog/2007/08/28/how-to-implement-a-magic-wand-tool/

https://github.com/stanislaushimovolos/Intelligent-Scissors

https://stackoverflow.com/questions/38985755/imitating-the-magic-wand-photoshop-tool-in-opencv

https://stackoverflow.com/questions/54554762/quick-selection-tool-algorithm

https://github.com/karlew/canvas-flood-fill
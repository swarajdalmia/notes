# Practical Vim 

Notes taken while reading "Practical VIM - edit text at the speed of thought" by Drew Neil (2nd edition).

To not source your vimrc on startup use:
`vim -u NONE -N` the -u NONE flag tells vimto nout source vimrc. When vim starts without a vimrc it reverts to vi compatible mode which causes many useful features to be disabled. Using the -N flag prevents this by setting the non-compatible option. 

To activate vim built in plugins one needs to use `set nocompatible` cause otherwise compatibility with vi is done and some essential features of vim are not included.  If a .vimrc already exists, one doesnt need to use it, but if uses a specific config using -u, then that config needs to contain `set nocompatible`.

The version of vim i am using is 8.1 with feature set normal. Everything is not included in that. Consider using huge version if necessary. 
 
## Chapter - 1: The VIM way 

Our work is repetitive by nature. Anything that can streamline a repetitive workflow will save our time multifold. Vim is optimized for repetition. Its efficiency stems from the way it tracks our most recent actions. We can always replay the last change with a single keystroke. Powerful as this sounds, it’s useless unless we learn to craft our actions so that they perform a useful unit of work when replayed. Mastering this concept is the key to becoming effective with Vim.

- dot command : The dot command lets us repeat the last change. It is the most powerful and versatile command in Vim. But first we have to ask, “What is a change?” A change could act at the level of individual characters, entire lines, or even the whole file. Motion commands are not taken as things to remember. Everytime one goes into insert mode, till one presses escape is counted as a change. So is saying using `>G` to indent. One can then go to the next line and press `.` to indent again. However, movement commands that put one in insert mode, for example 'A' will be redone as part of the last change on using dot. 

**macros** : Later we’ll see that Vim can record any arbitrary number of keystrokes to be played back later. This allows us to capture our most repetitive workflows and replay them at a keystroke. We can think of the dot command as being a miniature macro, or a “micro”.

An example of efficiently adding ; at the end of several lines is discussed next. Next an exmple of adding spaces around + is discussed. However motions are not repeatable, but here they are made repeatable using the find command `f+` and then using `;` to go to the next instance. 

When facing a repetitive task, we can achieve an optimal editing strategy by making both the motion and the change repeatable. Vim has a knack for this. It remembers our actions and keeps the most common ones within close reach so that we can easily replay them. 

 

 

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

![](./images/vim-repeatable.jpeg)

#### Be Lazy: Search Without Typing
The `*` command executes a search for the word under the cursor at that moment. Instead of using search and repeat replace one can use `n` to go to the next instance and then use . to redo the editing one did first time round. Use this to replace some of the words and not replace others. 

**The Ideal: One Keystroke to Move, One Keystroke to Execute**. It can’t really get any better than that, can it? It’s an ideal solution. We’ll see this editing strategy coming up again and again, so for the sake of convenience, we’ll refer to this pattern as the Dot Formula.

# Modes in VIM
Vim provides a modal user interface. This means that the result of pressing any key on the keyboard may differ depending on which mode is active at the time. It’s vital to know which mode is active and how to switch between Vim’s modes. In this part of the book, we’ll learn how each mode works and what it can be used for.
 
## Chapter - 2: Normal Mode
Normal mode is Vim’s natural resting state. Many Normal mode commands can be executed with a count, which causes them to be run multiple times.

Just because you can save keystrokes by using a count doesn’t mean that you should. We’ll look at some examples where it’s better simply to repeat a command than take the time to count how many times you want to run it. Much of the power of Normal mode stems from the way that operator commands can be combined with motions.

#### Granularity of Undo 
In other text editors, invoking the undo command after typing a few words might revert the last typed word or character. However, in Vim we can control the granularity of the undo command. From the moment we enter Insert mode until we return to Normal mode, everything we type (or delete) counts as a single change. So we can make the undo command operate on words, sentences, or paragraphs just by moderating our use of the <Esc> key. As a general rule, if you’ve paused for long enough to ask the question, “Should I leave Insert mode?” then do it. 

The best way to choose amonsgt possibilities is to see which is repeatable using the dot operator. IN the book we find the best way to delete a word given cursor is at the last character of the word. 

#### Don't count if you can repeat
We can minimize the keystrokes required to perform certain tasks by providing a count, but that doesn’t mean that we should. Consider the pros and cons of counting versus repeating.

The only advanatge of using count is having a cleaner undo history. 

#### Combine and Conquer
Much of Vim’s power stems from the way that operators and motions can be combined. `Operator + Motion = Action`. Type `:h operator` to find the operators in vim. The combination of operators with motions forms a kind of grammar. The first rule is simple: an action is composed from an operator followed by a motion.
Suppose that we already know how to delete a word using daw, and then we learn about the gU command (see :h gU   ). It’s an operator too, so we can invoke gUaw to convert the current word to SHOUTY case. 

Vim’s grammar has just one more rule: when an operator command is invoked in duplicate, it acts upon the current line. So dd deletes the current line, while >> indents it. The gU command is a special case. We can make it act upon the current line by running either gUgU or the shorthand gUU.

### Extending Vim’s Combinatorial Powers
The number of actions that we can perform using Vim’s default set of operators and motions is vast. But we can expand these even further by rolling our own custom motions and operators.

#### Custom operators and motions in VIM
If you’re curious about how to create your own custom operators, start by reading :h :map-operator

If you’re curious about how to create your own custom motions, start by reading :h omap-info

### Operator Pending Mode
Normal, Insert, and Visual modes are readily identified, but Vim has other modes that are easy to overlook. Operator-Pending mode is a case in point. We use it dozens of times daily, but it usually lasts for just a fraction of a second. For example, we invoke it when we run the command dw. It lasts during the brief interval between pressing d and w keys. Blink and you’ll miss it!
If we think of Vim as a finite-state machine, then Operator-Pending mode is a state that accepts only motion commands. It is activated when we invoke an operator command, and then nothing happens until we provide a motion, which completes the operation. While Operator-Pending mode is active, we can return to Normal mode in the usual manner by pressing escape, which aborts the operation

Many commands are invoked by two or more keystrokes but in most cases, the first keystroke merely acts as a prefix for the second. These commands don’t initiate Operator-Pending mode. Instead, we can think of them as namespaces that expand the number of available command mappings. 

Why, you might be wondering, is an entire mode dedicated to those brief moments between invoking operator and motion commands, whereas the namespaced com- mands are merely an extension of Normal mode? Good question! Because we can create custom mappings that initiate or target Operator-Pending mode.

## Chapter 3 : Insert Mode


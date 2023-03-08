# Makefile recipes in various languages

Using make does not mean that you have to learn shell scripting (altough it's always a good idea to have at least basic knowledge about it).


__You can use almost any scripting language for make recipes !__ 

@TODO: add note about linux philosophy (one toll - one job) => and so works make

@TODO: SHELL / .SHELLFLAGS configuration

## Examples

This repo provides some examples using make with pure 

- NodeJS
- Python
- SQLite3

__If you have some more ideas to showcase - create a pull request !__

### Usage

The execute them 

- `cd` into the desired example directory

- execute `make`

@TODO: add some more make settings we feel comforgtable with

# Opinionated tip: use `.RECIPEPREFIX`

make is a impressive but stone age old tool with a long history.

At the time of development (=> some decades ago 😅) their authors thought it's a good idea to use `'\t'` as recipe prefix.

The result is one of the most asked questions from `make` novices : 

> When executing my Makefile I get the following error
> 
> ```
> Makefile:xx: *** missing separator.  Stop.
> ```
>
> What does that error mean ? 

## What is the recipe prefix ?

A Makefile consists mostly of targets and their recipes. 

A target is usually a file/directory to be generated by the target recipe. 

An example: 

```make
foo.exe: foo.c
  cc -o foo.exe foo.c
```

The recipe prefix is the prefix starting each recipe line. 

__By default it is `'\t'`.__

And that's often a problem - because depending of the used editor / settings tabs may be converted to spaces. 

If you use spaces instead of tabs you get this mysterious error message : 

```
Makefile:xx: *** missing separator.  Stop.
```

## Solution

A solution to workaround that potential issue is to change the recipse prefix to something different : 

```make
# tell make to use '>' as recipe prefix
.RECIPEPREFIX = >

foo.exe: foo.c
> cc -o foo.exe foo.c
```

Now we have a visible character as recipe prefix which is much less error prone.

_The `.RECIPEPREFIX` directive is available since `make` version 4.0._

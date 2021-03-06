Formulas
========

Formulas are one of the core API objects in the Timeless Stack.
They're a [Layer 1](../design/API.md#layer-1) object in the big picture.

Formulas are a description of a container, as a pure function:
we list inputs (by hash, thus immutably), then describe a process,
and list what paths in the filesystem we want to save as outputs.


What's in a Formula?
--------------------

Formulas come in three parts:

```
{
	"inputs": {
		[... map of paths to WareIDs ...]
	},
	"action": {
		[... structure with commands and env ...]
	},
	"outputs": {
		[... set of paths we should save ...]
	}
}
```

Formula **inputs** and **outputs** are fairly straightforward; you can quickly get
a grasp of what they're representing if you've already understood the
[rio](../cli/rio.md) command and the [Layer 0](../design/API.md#layer-0) model
of [Wares](../glossary.md#Ware).

Formula **actions** can be thought of as roughly a shell script that runs in a
container which is populated with the filesets specified by the WareIDs in your
input section.  They also include many other fields:

- exec command
- environment vars
- uid/gid for exec
- working directory

More information about all the fields in an action, their details, and their
defaults are covered in further sections:

- [Formula Default Values](./defaults.md)
- [Formula Execution Policy](./policy.md)

(There's also a fourth section, called "context", which often accompanies
a formula.  The purpose of "context" is to carry around all the other incidental
details we need to make things runnable, like URLs where we expect to be able
to fetch the PackIDs of the inputs.  But since this is, well, *contextual* to
when and where we're evaluating the formula, we keep it separated.)

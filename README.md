dialogtree.js - clean and simple implementation of dialog tree in javascript

### What is a dialog tree ?

A
[Dialog tree](http://en.wikipedia.org/wiki/Dialog_tree)
is used in game to code the conversation the player may have with bots
(or [non playable characterer](http://en.wikipedia.org/wiki/Non-player_character)).

A dialog tree is in fact a graph, multiple answer may lead to the same questions.
In this tree, what is a node ? A dialog node encodes one exchange in the dialog.
1. Bot can say something. 
1. Player got multiple choises to pick
1. depending on player choise, we go to the next node
1. if there are no more children, the conversation is over

dialogtree.js handle the dialog tree itself, then you need a runner, aka a interface for the user to actually 
perform this dialog. You can find one in the /examples directory. This is a runner for js console: so you can use
it to run in the browser js console, or in node.js one.

### Future works

#### make text as template
  * string are template e.g. "Hello <%= playername %>"
  * microtemplate.js ?

#### make a graphical editor
* currently the dialog tree is a array encoding in json
* to edit that in a text file is doable but may rapidely become very inconfortable
* it is ok on very short/simple conversation
* for longer one, a graphical editor is likely needed
  * it has to be webbased obviously
  * how to do it easily ? (ui, load/save, with server or not)
  
### Samples
Here is a sample of dialog encoded in json. This is the one used in /example

```
[
	{
		"nodeId"	: "initialQuestion",
		"botText"	: "hello, how are you ?",
		"answers"	: [
			{
				"playerText"	: "fine! and you ?",
				"nextNodeId"	: "nodeHappyDay"
			},
			{
				"playerText"	: "I have a terrible day...",
				"nextNodeId"	: "nodeBadDay"
			}
		]
	},
	{
		"nodeId"	: "nodeHappyDay",
		"botText"	: "me too! how can i help you ?",
		"answers"	: [
			{
				"playerText"	: "Just be happy, it is enougth for me!",
				"nextNodeId"	: null
			},
			{
				"playerText"	: "You can help me kill one guy, i need cash!",
				"nextNodeId"	: "nodeAboutToDie"
			},
		],
	},
	{
		"nodeId"	: "nodeBadDay",
		"botText"	: "oh really ? sad to hear that. How come ?",
		"answers"	: [
			{
				"playerText"	: "i mistune my clock so i missed my train... ",
				"nextNodeId"	: "nodeNoClock"
			},
			{
				"playerText"	: "im gonna die today. i know it",
				"nextNodeId"	: "nodeAboutToDie"
			},
		],
	},
	{
		"nodeId"	: "nodeNoClock",
		"botText"	: "You looser you dont even know how to tune a clock. how ridicous, steer away",
		"answers"	: [
			{
				"playerText"	: "you are so unfair!",
				"nextNodeId"	: null
			},
		],
	},
	{
		"nodeId"	: "nodeAboutToDie",
		"botText"	: "You seems like dangerous to be around. So Long.",
		"answers"	: [
			{
				"playerText"	: "ah ? well see ya",
				"nextNodeId"	: null
			}
		]
	},
]
```

#### Some Links 
* video about dialog tree
  * http://www.youtube.com/watch?v=lF5ipjVA_Ls
  * http://www.youtube.com/watch?v=h7XsZXJor7A
  * http://www.youtube.com/watch?v=A0R34QPp9gc
  * http://www.youtube.com/watch?v=_vLq7p-a6MM
* related techno
  * http://en.wikipedia.org/wiki/Digital_conversation
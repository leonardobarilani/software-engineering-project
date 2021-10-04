# Game rules implementation

To implement the rules of the game we took inspiration from the Bytecode Pattern.

All the rules are implemented through minimal instructions, thus the whole game is represented by a sequence of instructions executed by the server.

## List of instructions

Instructions are written in JSON syntax (just the instruction followed by the parameters); here are written in a more human readable format.

### Move

> `MOVE quantity FROM startpoint BY starthow TO endpoint BY endhow`

Move dice from a container of dice to another.

* `quantity`: either a number of dice (implying the user has to specify how many) or string `all`
* `startpoint/endpoint`: where to get/put the dice. It is not possible to specify the same container. At least one container must be `current`. Possible containers: `current`, `pool`, `board`, `bag`, `track`
* `starthow/endhow`: specify how to take the dice. `user`, `random`, `append` (useful only for the roundtrack and current)

### Control

> `CONTROL player`

Put the specified player in control of the inputs (it is that player turn).

* `player`: player's id

### Tool

> `TOOL option`

Generate the instructions for a tool.

* `option`: either `draft`/`nodraft`. The player can use a draft tool or a non-draft tool

### Round

> `ROUND direction`

Change the rotation of the turns (clockwise/counter-clockwise)

* `direction`: either `forward`/`backward`

### Rotate

> `ROTATE`

Set the new first player for the round that is about to begin ("give" the dicebag to that player).

### Restriction

> `RESTRICTION what FROM this TO that`

Some toolcards allow the users to modify the dice (e.g. change the number of it). This instruction "restrict" these changes, specifying what changes can be made (for example if a 1 can become a 6 or not and so on)

* `what`: string `number`
* `this`: a number
* `that`: a number

### Input

> `INPUT FROM here FROM here`

Allow a user to make choices. The numer of parameters is dynamic, can be one or more.

* `here`: name of containers where the user can pick something. Can also be `choose` to make a choice

### Modify

> `MODIFY how`

Modify the content of `current` based on the rules specified by `RESTRICTION`.

* `how`: either `user` or `random`. `user` will modify the first dice in `current`, `random` will modify all dice in `current`

### Reset

> `RESET what`

Reset the some MicroOperationVariables.

* `what`:
  * `restrictions`: clear the restrictions set with `RESTRICTIONS`
  * `choose`: clear the current schema variable
  * `input`: clear the input variables

### Filter

> `FILTER filters USED value`

Enable or disable a filter; filters are the rules to place dice on boards

* `filters`:
  * `emptycell`: a die can't be placed on an occupied cell
  * `dienumber`: a die can't be placed next to a die with the same number
  * `diecolor`: a die can't be placed next to a die with the same color
  * `boardnumber`: a die must be placed obeying numbers board restriction
  * `boardcolor`: a die must be placed obeying colors board restriction
  * `neardie`: a die must be placed near another die
  * `fullcell`: a cell that contains a die must be selected
  * `roundtrackfullcell`: a cell on the round track that contains a die must be selected
* `value`: either `yes` or `no` to enable/disable the policy

### Program

> `PROGRAM program`

Load the specified `program` file after the current instruction

### Subfavours

> `SUBFAVOURS number`

Subtract the specfied amount of favours from the current player (player in `CONTROL`)

### Choose

> `CHOOSE option`

Let the player choose the board schema

### Checkpoint

> `CHECKPOINT`

This instruction commits the actions of the current player

## Example of program: Tool 2

> Tool 2: move any die in your board ignoring color restrictions. All others restrictions must be obeyed

```json
{"microOperationList":[
  {"type":"checkpoint", "parameters":[]},
  {"type":"subfavours",   "parameters":["2"]},
  {"type":"program",  "parameters":["src/main/resources/programs/reset_filters"]},
  {"type":"reset", "parameters":["input"]},

  {"type":"filter", "parameters":["fullcell","yes"]},
  {"type":"input", "parameters":["board"]},
  {"type":"filter", "parameters":["fullcell","no"]},
  {"type":"move", "parameters":["1","board","user","current","append"]},

  {"type":"filter", "parameters":["emptycell","boardnumber","dienumber","diecolor","neardie","yes"]},
  {"type":"input", "parameters":["board"]},
  {"type":"filter", "parameters":["emptycell","boardnumber","dienumber","diecolor","neardie","no"]},
  {"type":"move", "parameters":["all","current","random","board","user"]},
  {"type":"checkpoint", "parameters":[]}
]}
```

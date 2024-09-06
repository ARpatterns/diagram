# AR Pattern Diagram

## Introduction

In order to provide a compact visualization of active Event-Condition-Action (ECA) rules we developed a diagram representation consisting of rule-reaction blocks. AR pattern diagrams can be seen as a kind of pseudo code representation for Augmented Reality programs. The first line of a rule-reaction block in such a diagram shows the active rule as an Event-Condition-Action triple. Following the rule is a blockquoted line that depicts the changed state as reaction. 

| Event | Condition | Action |
|---|---|---|
> changed state or reaction

If no condition is defined, it evaluates to true, and the diagram shows an immediate execution arrow (&rarr;). 

| Event | &rarr; | Action |
|---|---|---|
> changed state or reaction

To illustrate the use of the diagram, consider the following example which presents an active rule triggered by a temporal event (in 20 seconds). If no item is found in the current AR session (the condition), the action will provide a voice feedback (the reaction) using a text-to-speech system.

| in:20 sec | if:`items.@count == 0`| do:say |
|---|---|---|
> "You may add an item!" 🗣

An action may dynamically load and run new consecutive rules. These rules are displayed as indented block quotes consisting of one or several sequential rules. All rules in a block are loaded and installed in sequence, yet not (all) executed at loading time, but triggered by their corresponding event. 

| on:start |  &rarr;  | do:request |
 |---|---|---|
> &darr; _do:run_ &larr; _on:response_ ••• $SERVER/actions/doit.json 
> | on:command |  &rarr; | do:assign |
> |---|---|---|
>> `data.flag = 1`
> 
> | in:5 sec |  &rarr; | do:assign |
> |---|---|---|
>> `data.flag = 0`
> 

## Markdown Mappings for AR Pattern Diagrams

The AR pattern diagram has been designed to be technology-agnostic. It can be created straightforward in the Markdown language and rendered as styled text. With this easy to use solution, AR patterns may be seamlessly incorporated into the authoring process, ultimately improving both documentation and communication of AR programs.

The mapping to Markdown used to create AR Pattern diagrams is defined in the following by the Markdown code and its rendering.

### ECA Block

```markdown
| Event | Condition | Action |
|---|---|---|
> changed state or reaction
```

| Event | Condition | Action |
|---|---|---|
> changed state or reaction

### ECA Rule Symbols

| on/in/as:___ | if:___ | do:___ |
|---|---|---|

### Text Styles
- __Bold__: Text in the ECA block (need no MD coding, because first row in table is bold anyway; otherwise ``__Bold__``)
- `Courier`: predicates, expressions and program code executed at runtime  (`` `Courier` ``)
- _Italic_: ECA rules that are not explicitly coded but are added automatically (`_Italic_`)


### Text Quoting

- 'Single Quotes': identifiers
- "Double Quotes": text strings
- None: all other text


### Condition Symbol
- always true: &rarr; (`&rarr;`)


### Block Quoting

An action may dynamically load and run new consecutive rules. These rules are displayed as indented block quotes consisting of one or several sequential rules. 
Dynamically loaded rules may be called hierarchically leading to nested blocks. (`>`, `>>`, ...)

```markdown
| on:command | &rarr; | do:detect:feature |
|---|---|---|
> Install feature detector &larr; "chair" 👁
> | _on:detect_ | &rarr; | _do:execute:op_ |
> |---|---|---|
> 
> > `say('I found a chair')`  
> 
```

 | on:command | &rarr; | do:detect:feature |
 |---|---|---|
> Install feature detector &larr; "chair" 👁
> | _on:detect_ | &rarr; | _do:execute:op_ |
> |---|---|---|
> 
> > `say('I found a chair')`  
>

 
### Reaction Symbols (optional)
- do:add: ➕
- do:remove: ✘
- do:say: 🗣
- do:play: 🔈
- do:stop: ◾
- do:replace 'id1' ⬅ 'id2'
- do:detect: 👁

## Sample Diagrams

**Conditional Reaction Pattern**

```markdown
| in:7 sec | if:`location.city == 'Berlin'`| do:say |
|---|---|---|
> "Hello Berlin!" 🗣
```

| in:7 sec | if:`location.city == 'Berlin'`| do:say |
|---|---|---|
> "Hello Berlin!" 🗣

---

**AR Scenario using several AR Patterns**

```markdown
| at:start| &rarr; | do:request GET:JSON |
|---|---|---|
> &darr; _do:run_ &larr; _on:response_ ••• $SERVER/detectors/detectMarker.json
> | on:command | &rarr; | do:detect:image |
> |---|---|---|
> 
>> Install image detector 0.1x0.1 &larr; _on:response_  •••  marker.png 👁
>> | _on:detect_ | &rarr; | _do:add to AR anchor_ |
>> |---|---|---|
>> 
>>> 'scene.3D' ➕
>> 
>> | _as:stated_ | _if:`visible('scene.3D') == false`_ | _do:remove_ |
>> |---|---|---|
>> 
>>> 'scene.3D' ✘
>
```

| on:start| &rarr; | do:request GET:JSON |
|---|---|---|
> &darr; _do:run_ &larr; _on:response_ ••• $SERVER/detectors/detectMarker.json
> | on:command | &rarr; | do:detect:image |
> |---|---|---|
> 
>> Install image detector 0.1x0.1 &larr; _on:response_  •••  marker.png 👁
>> | _on:detect_ | &rarr; | _do:add to AR anchor_ |
>> |---|---|---|
>> 
>>> 'scene.3D' ➕
>> 
>> | _as:stated_ | _if:`visible('scene.3D') == false`_ | _do:remove_ |
>> |---|---|---|
>> 
>>> 'scene.3D' ✘
> 

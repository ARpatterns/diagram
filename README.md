# AR Pattern Diagram

## Introduction

... todo

## Markdown Mappings for AR Pattern Diagrams

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
- None: all other texts

### Block Quoting

An action may dynamically load and run new rules. These rules are displayed as indented blockquote. 
All rules in a block are loaded and installed in sequence, yet not (all) executed at loading time, but triggered by their corresponding event.
Dynamically loaded rules may be called hierarchically leading to nested blocks. (`>`, `>>`, ...)

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
>> | _as:stated_ | _if:`function('scene.3D', 'visible') == false`_ | _do:remove_ |
>> |---|---|---|
>> 
>>> 'scene.3D' ✘
> 

### Condition Symbol
- always true: &rarr; (`&rarr;`)
 
### Action Symbols (optional)
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

**Request-Response Pattern**

```markdown
 | on:command | &rarr; | do:detect:feature |
 |---|---|---|
 
> Install feature detector &larr; "chair" 👁
> | _on:detect_ | &rarr; | _do:execute:op_ |
> |---|---|---|
> 
> > ``function('I found a chair', 'say')`  
> 
```

 | on:command | &rarr; | do:detect:feature |
 |---|---|---|
 
> Install feature detector &larr; "chair" 👁
> | _on:detect_ | &rarr; | _do:execute:op_ |
> |---|---|---|
> 
> > `function('I found a chair', 'say')`  
>

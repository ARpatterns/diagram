# AR Pattern Diagram

## Markdown Mappings for AR Pattern Diagrams

### ECA Block

| Event |  Condition | Action |
 |---|---|---|
> changed state or reaction

### ECA Rule Symbols

| on/in/as:___ |  if:___ | do:___ |
 |---|---|---|

### Text Styles
- __Bold__: Text in the ECA block (need no MD coding, because first row in table is bold anyway; otherwise ``__Bold__``)
- `Courier`: predicates, expressions and program code executed at runtime  (`` `Courier` ``)
- _Italic_: ECA rules that are not explicitly coded but are added automatically (`_Italic_`)


### Block Quoting


### Text Quoting

- 'Single Quotes': identifiers
- "Double Quotes": text strings
- None: all other texts

### Condition Symbol
- always true: &rarr; (`&rarr;`)
 
### Action Symbols (optional)
- do:add: ➕
- do:say: 🗣
- do:play: ◀
- ...

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
 | on:command |  &rarr; | do:detect:feature |
 |---|---|---|
 
> Install feature detector &larr; "chair" 👁
> | _on:detect_ | &rarr; | _do:execute:op_ |
> |---|---|---|
> 
> > ``function('I found a chair', 'say')`  
> 
```

 | on:command |  &rarr; | do:detect:feature |
 |---|---|---|
 
> Install feature detector &larr; "chair" 👁
> | _on:detect_ | &rarr; | _do:execute:op_ |
> |---|---|---|
> 
> > `function('I found a chair', 'say')`  
>

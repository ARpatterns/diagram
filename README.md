# AR Pattern Diagram

## Sample Diagrams

**Conditional Reaction Pattern**

```markdown
| in:7 sec | if:location.city == 'Berlin'| do:say |
|---|---|---|
> "Hello Berlin!" 🗣
```

| in:7 sec | if:location.city == 'Berlin'| do:say |
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
> > function('I found a chair', 'say') ◀  
> 
```

 | on:command |  &rarr; | do:detect:feature |
 |---|---|---|
 
> Install feature detector &larr; "chair" 👁
> | _on:detect_ | &rarr; | _do:execute:op_ |
> |---|---|---|
> 
> > function('I found a chair', 'say') ◀  
>

## Markdown Mappings for AR Patterns Diaagram

### ECA Block

| __Event__ |  __Condition__ | __Action__ |
 |---|---|---|
> changed state or reaction


### Text Styles
- __Bold__: Text in the ECA block (``__Bold__``)
- `Courier`: predicates, expressions and program code executed at runtime  (`` `Courier` ``)
- _Italic_: ECA rules that are not explicitly coded but are added automatically (`_Italic_`)
-  

### Block Quoting


### Text Quoting

- 'Single Quotes': identifiers
- "Double Quotes": text strings
- None: all other texts

### Condition Symbol
- always true: &rarr; (`&rarr;`)
- 
### Action Symbols (optional)
- do:add: ➕
- do:say: 🗣
- ...



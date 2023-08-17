# AR Patterns Diagram

## Test Diagram

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

```markdown
**Request-Response Pattern**

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




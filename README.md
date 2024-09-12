# AR Pattern Diagram

## Introduction

AR pattern diagrams can be seen as a kind of pseudo code representation for Augmented Reality functionalities. They work as a rough documentation and help to comprehend the triggering, decision control, and execution mechanism of AR behavior.
AR experiences are heavily driven by elements detected in the real world, without having control over their occurrence and timing during the creation process. The reactive behavior and dynamic scenography of AR/MR experiences are therefore modeled as event-driven reactions described as [Event-Condition-Action](https://github.com/ARpatterns/catalog/tree/main/eca) (ECA) rules that perform an action in response to an event, provided that certain conditions are met. In the context of AR patterns, ECA rules build a generic technology-agnostic abstraction of the reactive behavior of AR software systems.

Together with visual [illustrations](https://arpatterns.dev/illustrations) of the scene, AR pattern diagrams help teams stay productive by making it easier to: 
- Navigate AR scenarios without reading source code.
- Plan out new features before programming.
- Quickly onboard new team members.
- Collaborate with technical and non-technical team members.


## Rule-Reaction Block

In order to provide a compact visualization of active Event-Condition-Action (ECA) rules we developed a diagram representation consisting of rule-reaction blocks. The first line of a rule-reaction block in such a diagram shows the active rule as an Event-Condition-Action triple. Below the rule a blockquoted line follows which depicts the changed state as reaction. 

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

Several ECA rules may be loaded and installed at the same time. They are shown as sequences of rule-reaction blocks. Be aware that they are installed at the same time but may not be triggered at the that time.

| on:stable |  &rarr; | do:add ahead 0.0 1.0 -0.9 |
|---|---|---|
> 'red.box' ➕

| on:stated | if:`visible('red.box') == true`| do:say |
|---|---|---|
> "you see a red box" 🗣
 
| on:stated | if:`visible('red.box') == false`| do:say |
|---|---|---|
> "now you don't" 🗣


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

## How to write an AR Pattern Diagram?
1. List the items that will augment the real world as media assets (e.g., 3D models, parametric geometries, images, audio files, text). These items should then be taggled by ECA rules.
2. Enumerate potential events that may occur during the AR session and will trigger behavior and interactivity. See typical [Events in AR applications](https://github.com/ARpatterns/catalog/blob/main/eca/events.md).
3. Arrange the enumerated items and events into Event-Condition-Action rules that will manipulate media items, run-time data, and system settings. 
4. Whenever possible use the generic action identifiers listed in [Actions in AR Applications](https://github.com/ARpatterns/catalog/blob/main/eca/actions.md)
5. Depict the reaction of the triggered action.
6. Write down the rule-reaction blocks in [Markdown](https://www.markdownguide.org) by applying the corresponding [styling](#markdown-mappings-for-ar-pattern-diagrams). 
7. Integrate and render the diagram as embedded documentation, e.g., in README files within github repositiories or in Web-based technical documentations. 


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

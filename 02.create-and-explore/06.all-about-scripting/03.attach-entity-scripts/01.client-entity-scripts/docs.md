---
title: Create Client Entity Scripts
taxonomy:
    category: docs
---

By attaching a client script to an entity, you can have entities that respond to events. For example, you could have an entity that changes color when clicked on.

There can be many entities in a domain, and each can have a different associated client entity script. These run in the same environment and namespace in Interface. To preserve modularity, entity scripts are defined as an anonymous JavaScript function definition. Interface then evaluates that function to create an object for each scripted entity, with methods on it.

For example, here is a client entity script, `changeColorOnClickDown.js`, which when attached to a non-model entity like a box or sphere, will change the color of the entity when you click on it.

```
 1 //  changeColorOnClickDown.js
 2 (function () { 
 3     var clicked = false;
 4     this.clickDownOnEntity = function (entityID, mouseEvent) { 
 5         if (clicked){
 6             Entities.editEntity(entityID, { color: { red: 0, green: 255, blue: 255} });
 7             clicked = false;
 8         } else {
 9             Entities.editEntity(entityID, { color: { red: 255, green: 255, blue: 0} });
10             clicked = true;
11         }
12     }; 
13 })

```

You'll notice that this example is written as a JavaScript class prototype function. You'll also notice that it uses the mouse event [clickDownOnEntity()](https://wiki.highfidelity.com/wiki/ClickDownOnEntity()). When the user clicks on an entity, `clickDownOnEntity()` triggers the function associated with that click event. In this case, it edits the entity's color back and forth between yellow and magenta.

To learn more:

- For more information on events available, see the High Fidelity [Category:JavaScript_API](https://wiki.highfidelity.com/wiki/Category:JavaScript_API).
- For a walk though of additional examples, see [entity script examples](https://wiki.highfidelity.com/wiki/Entity_script_examples).
- For a list of event methods that may be defined, see [Category:Entities_callbacks](https://wiki.highfidelity.com/wiki/Category:Entities_callbacks), [preload()](https://wiki.highfidelity.com/index.php?title=Preload()&action=edit&redlink=1), and [unload()](https://wiki.highfidelity.com/index.php?title=Unload()&action=edit&redlink=1)
- For more examples, see the [GitHub repository](https://github.com/highfidelity/hifi/tree/master/scripts/tutorials).

Now that we have a script, for it to do anything, you need to attach it to an entity. See [Attaching Entity Scripts](https://wiki.highfidelity.com/wiki/Attaching_Entity_Scripts).
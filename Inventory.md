# Inventory System

The idea of the Inventory System is to create a flexible way for the player to store itens in an intelligent fashion.
It should consist of a main window where all owned items are displayed with a quantity, and the possibility to see it's description.
The system should be flexible enough to allow the Character to carry a maximum number of itens based on slots. (since this is the same system used by the Table Top mechanic)

By defaut, the idea is that each Character in the party adds 4 slots to the maximum number of itens to be carried.
Since the party can hold a maximum of 3 characters, that would means in a maximum limit of 12 items, including non-equipped equipments like Swords and Armors, Potions, Loots from enemies and etc.
The only type of item that doesn't occupy Slots are Quest items, which are hold in a separate bag with infinite size.

Specific characters classes can have extended Inventory Limits, like Merchants and Tankers.
Itens stack in quantity but they must be the same type. Which means that potions and super potions are carried in separate slots.

Different from games like Diablo, all Itens share generally the same size in the inventory (Virtually talking), 
which means a Full Plate and a Monster Feather will both occupy 1 single slot.
However, itens considered REALLY big, like a Huge Bag of Beans, or a Stone Statue may occupy more than 1 slot. (sometimes even slots).

One interesting thing not entirely related to the Inventory system, is that some items will appear visually in the characters just by being inside the inventory.
This is the case for huge items (like animals and stone statues), and some special items that may emit some kind of aura 
(ex: a badly Rotten Food which can be lying in your inventory can generate a green aura, signaling to the player that he perhaps have to check the state it's items)
Also, this can have interesting side effects in the game, like attracting more monsters, or making the monsters more aware of your presente. (or even generating bonuses in battle)

It's important to state that, although each one of the characters have a share in slots to add to the party, the inventory system is used as a single stash of itens, never being separeted per character.
 
A few features would include:

- Export the entire Inventory System as a single and simple component to be used in other scenes.
- Allow to open and close Inventory passing a Keycode in the inspector.
- Allow Keycode to be configured easily in the inspector.
- Create Scriptable Object to represent items. This object must include the icon of the item as well.
- Drag & Drop system to allow drop itens into the ground.
- Drag & Drop system to allow itens to be re-organized in the inventory window.
- Visually display dynamically the number of slots configured in the component.
- Create Event system to allow other Components to interact with the Inventory System, adding, activating, consuming and droping items.
- Create Click system to allow Itens to be used.
- Allow each item to also have script that will describe what happens when the item is used, droped or picked up.

# Breaking the Inventory System into MVP

Since the Inventory system have a lot of complexity, it would be interesting to break down complexity by creating simplifying versions of the Component, and then escalate accordingly.
I will describe here some levels of iteractions that we can have with this component.

## Part 1 - Proof of Concept, Data Properties of an Inventory

In this part 1, we are not worried with a Physical and Visual Inventory.
All we want is to be able to control the Bag via script and to have a single InventoryPreferences object that will act as the "Global variable" of the Inventory.

A few features we want:

- A Scriptable Object to work as the "InventoryPreferences", acting as a global variable that can hold the current state of the Inventory.
- A Scriptable Object Item component that will act as each Item configuration. Initially, it should have only Name, Description and an Icon. Later we can think about other properties.
- The InventoryPreferences will hold an Array of Item objects, and through the Object Methods, we will be able to implement some basic operations like:
  - Add one Item to a Slot
  - Stack Quantity of Items in the Slots
  - Remove one item in a given Slot
  - Make it possible to limit the number of Itens in the Inventory, by setting a `maxSlots` property.

This Scriptable object will have methods to control the Bag, 

## Part 2 - A basic, visual Inventory

In the part 2, the important is to have the basic behavior of an Inventory, which includes:

- A window to store itens in the Inventory
- A Slot component which will act as a holder, with an Item property and a Quantity property.
- A grid to display the Slots visually.

In this first version of the UI, we are not worried in implementing the InventoryPreferences, this is only the visual barebones to implement Part 3.

## Part 3 - Integrating InventoryPreferences

Here we want to integrate our work in the Part 1 (which a Code-Only), and our work in Part 2 (which is Visual-only)
This approach make it easy to reason about each part, and create the separation we need to build a smart component.

Here we want to reflect the Data inside the InventoryPreferences into the Slots.
So things we would want to do:

- Build dynamically the slots based on the number of `maxSlots` configured by the InventoryPreferences.
- Assign each visual slot dynamically to one virtual slot contained in the array of InventoryPreferences.
- Display the Item Icons and quantity of each slot.

## Part 4 - Implementing Events

Here we want trigger events in the InventoryPreferences.
Most of updates can be handle by `update` event, since all places are accessing the contents of `InventoryPreferences`.
However, a few actions like Drag n Drop requires extra work to setup.
For this, each item object must have a Drag and a Drop event that can be trigger when Player try to swap itens in the inventory, or move them to empty slots.
This could be possible by simply sending an update the InventoryPreferences, updating the Slots contents. (it could even be a helper in the InventoryPreferences).
Adopting this strategy is useful, because we don't need to ask the item to physically change the items, we could just ask InventoryPreferences to do the change, and once it's done, the `update` method on the Inventory component would automatically reflect the changes into the window. 

- Implement Drag event on Item
- Create a Ghost Item icon instead of moving the actual item. (search: ghost drag and drop)
- Implement Drop event on Item, to send Swap request to `InventoryPreferences`.
- Implement Drop event on Item, so Items moved outside the window can request removal to `InventoryPreferences`.
- Implement Double Click event on Item, so Items clicked can activate an effect defined on the Item Script. (defined per script)

## Diagram

A Diagram explaining this system could be described like this:

![image](https://user-images.githubusercontent.com/68507/105080051-0bc10180-5a6f-11eb-9ce6-a2fc8de70e49.png)

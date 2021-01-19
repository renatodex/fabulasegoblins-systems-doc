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

W.I.P

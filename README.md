# MMORPG DB Project Cover Page

### Date: Aug,5, 2024

### GroupNumber: 26

## 1) Description

For this project we are proposing a user database for an MMORPG (massive multiplayer online
role playing game) similar in scale and scope to well known titles like “the world of warcraft” and “final fantasy online”. In theory this would mean that the database would be responsible for the player data of 10,000,000+ player accounts as well as the inventory status and ranking of
any characters created under a player account.

The database of which we are going to use for this project is Oracle. We will also utilize: Java version 17, Java spring for GUI, and GIT for version control.

The database will be responsible for keeping track of the active player base’s data in regards to account creation, character creation, inventory management and ranking. As such users of the database (players of the game) will need to be able to create their own player accounts by submitting an email address, setting a username and password and then verifying their email address. Each account will be given a unique user ID and a friends list. Players will be able to add users to their friends list and track their online status and which character they are playing on.

Once an account has been verified, players should then be able to create character profiles. When creating a character, the player will need to give them a name, dec de on race and class, and customize the character’s physical attributes like height, weight, age, hair, facial structure. Each character will have an inventory, currency tracker, a unique charac er id a d a set of stats representing strength, intelligence, dexterity, charisma, and luck. 

A character’s inventory will hold a set number of slots for carrying items. Accounts will also be given 1 shared inventory that every character belonging to that account will be able to access. A character’s inventory can be filled with items. Items come in 4 major types; key items, consumables, equipment, and resources. Key items are quest specific items that have unique uses in the story or questline and can be any of the other 3 types in addition to being a key item. Consumables are single use items that typically provide the character with stat boosts or healing. Equipment are items that can be equipped to increase a character's stats and come in 6 types; chest, head, weapon, leg, boots, trinket. A character can carry multiple pieces of equipment but can only equip one of each type at a time. Resources are items that can be used at vendors to create other items. Consumables and resources can be “stacked” in a count only
taking up 1 inventory slot, equipment may not. All item’s have an item id.

After a user has created a character they can then decide on a server/region the character will start on. Each server/region will need to keep track of the characters that exist on the server and their fame. Each server has a name and location. Fame is a statistic used to give an individual player a ranking, given to players for completing quests or participating in special events. A character will be able to migrate between servers but will not migrate their fame with them. Each server will have a leaderboard of the characters with the most fame on the server, and there will be a world leaderboard for the characters with the most fame across all servers.


## 2) ER Diagram
![ER Diagram](/Final%20ER%20diagram.drawio.png)


## 3) Database Schema

### Accounts
| Attribute | Type | Constraints |
|-----------|------|-------------|
| username | VARCHAR(20) | PK |
| password | VARCHAR(20) | NOT NULL |
| email | VARCHAR(320) | UNIQUE and NOT NULL |
| isVerified | BOOL | |
| InvSlots | INT | NOT NULL, DEFAULT is 150 |

### Friends
| Attribute | Type | Constraints |
|-----------|------|-------------|
| user | VARCHAR(20) | PK, FK referencing accounts username ON CASCADE DELETE |
| friend | VARCHAR(20) | PK, FK referencing accounts username ON CASCADE DELETE |

### Characters
| Attribute | Type | Constraints |
|-----------|------|-------------|
| ID | CHAR(20) | PK |
| AccUser | VARCHAR(20) | PK, FK to Account's Username On Delete Cascade |
| name | VARCHAR(20) | NOT NULL |
| ServerName | VARCHAR(20) | FK to Servers name |
| class | VARCHAR(20) | NOT NULL |
| age | INT(2) | NOT NULL |
| height | INT(3) | NOT NULL |
| weight | INT(3) | NOT NULL |
| race | VARCHAR(20) | NOT NULL |
| strength | INT(5) | NOT NULL, DEFAULT is 1 |
| intelligence | INT(5) | NOT NULL, DEFAULT is 1 |
| charisma | INT(5) | NOT NULL, DEFAULT is 1 |
| dexterity | INT(5) | NOT NULL, DEFAULT is 1 |
| luck | INT(5) | NOT NULL, DEFAULT is 1 |
| level | int(5) | NOT NULL, DEFAULT is 1 |
| money | INT(15) | NOT NULL, DEFAULT is 0 |
| InvSlots | INT(2) | NOT NULL, DEFAULT is 50 |

### Equipped
| Attribute | Type | Constraints |
|-----------|------|-------------|
| AccUser | VARCHAR(20) | PK, FK to character's ID,AccUser ON DELETE CASCADE |
| CID | CHAR(20) | PK, FK to character's ID,AccUser ON DELETE CASCADE |
| EqName | VARCHAR(20) | PK, FK referencing equipments Name,Type ON UPDATE CASCADE and ON DELETE CASCADE |
| EqType | VARCHAR(20) | PK, FK referencing equipments Name,Type ON UPDATE CASCADE and ON DELETE CASCADE, NOT NULL |

### InventorySlots
| Attribute | Type | Constraints |
|-----------|------|-------------|
| CID | CHAR(20) | PK, FK to character's ID,AccUser Cascade ON Delete |
| AccUser | VARCHAR(20) | PK, FK to character's ID,AccUser Cascade ON Delete |
| slotNum | INT(3) | PK, unique |
| stacks | INT(4) | DEFAULT = 1 |
| itemName | VARCHAR(20) | FK to item's name, type |
| itemType | VARCHAR(20) | FK to item's name, type |

### SharedInventorySlots
| Attribute | Type | Constraints |
|-----------|------|-------------|
| AccUser | VARCHAR(20) | PK, FK referencing Account's Username, ON Delete Cascade |
| slotNum | INT(3) | PK, unique |
| stacks | INT(4) | DEFAULT = 1 |
| itemName | VARCHAR(20) | FK to item's name, type |
| itemType | VARCHAR(20) | FK to item's name, type |

### Items
| Attribute | Type | Constraints |
|-----------|------|-------------|
| name | VARCHAR(20) | PK |
| type | VARCHAR(20) | PK |
| isKey | BOOL() | DEFAULT is 0 |
| description | MEDIUMTEXT() | |

### Consumables
| Attribute | Type | Constraints |
|-----------|------|-------------|
| itemName | VARCHAR(20) | PK and FK to items name, type ON DELETE CASCADE ON UPDATE CASCADE |
| itemType | VARCHAR(20) | PK and FK to items name, type ON DELETE CASCADE ON UPDATE CASCADE |
| maxStack | int(2) | |

### Equipments
| Attribute | Type | Constraints |
|-----------|------|-------------|
| itemName | VARCHAR(20) | PK and FK to items name, type ON DELETE CASCADE ON UPDATE CASCADE |
| itemType | VARCHAR(20) | PK and FK to items name, type ON DELETE CASCADE ON UPDATE CASCADE |
| strength | INT(5) | |
| intelligence | INT(5) | |
| charisma | INT(5) | |
| dexterity | INT(5) | |
| luck | INT(5) | |

### Resources
| Attribute | Type | Constraints |
|-----------|------|-------------|
| itemName | VARCHAR(20) | PK and FK to items name, type ON DELETE CASCADE ON UPDATE CASCADE |
| itemType | VARCHAR(20) | PK and FK to items name, type ON DELETE CASCADE ON UPDATE CASCADE |
| maxStack | int(2) | |

### LeaderBoards
| Attribute | Type | Constraints |
|-----------|------|-------------|
| Location | VARCHAR(20) | PK |

### Participates
| Attribute | Type | Constraints |
|-----------|------|-------------|
| AccUser | CHAR(20) | PK |
| CID | CHAR(20) | PK, FK to characters id ON DELETE CASCADE |
| boardLoc | CHAR(20) | PK, FK leaderboards location |
| fame | INT | |

### Servers
| Attribute | Type | Constraints |
|-----------|------|-------------|
| name | VARCHAR(20) | PK |
| location | VARCHAR(20) | FK to leaderboards location |
| capacity | INT(6) | |

## Additional Constraints (not modeled by ER diagram)

- An account can be unverified but a character cannot be created until an account is verified
- Must check and decrement character/Account Inv slots before inserting into Inventory/sharedInventory or increment when deleting rows the slots should reflect how many spaces of inventory the character has in some way whether that's a counter or checked against slotNum.
- A single leaderboard represents the rankings for a single server location, ie. EU, US, CHN, KOR, not the individual servers ie. KOR - server1, KOR - server2 etc.
- A character belongs to only one server at a time, but is able to switch servers and accumulate fame local to that server's location.


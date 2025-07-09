---
title: Recipe Book
excerpt: Where to find common data objects and logic in the World Chain Contracts
tags:
  - ecosystem
  - eve
  - development
date: July 9th, 2025
create: July 9th, 2025
update: July 9th, 2025
---
# Data in tables
### Solidity
To read data from tables within Solidity - import the table from the relevant NPM package exporting the table.
Examples:
```solidity
import { Characters } from "@eveworld/world-v2/src/namespaces/evefrontier/codegen/tables/Characters.sol"

uint256 characterId = 1;
uint256 tribeId = Characters.getTribeId(characterId)
```
## Characters

### Get Character ID By Address
[MUD Explorer](https://explorer.mud.dev/pyrope/worlds/0xcdb380e0cd3949caf70c45c67079f2e27a77fc47/explore?tableId=0x746265766566726f6e746965720000004368617261637465727342794163636f&query=SELECT+%22account%22,+%22smartObjectId%22+FROM+%22evefrontier__CharactersByAcco%22+LIMIT+100+OFFSET+0;&page=0&pageSize=100)
Fetch `characterId` by account `address` using the `CharactersByAcc` table.

### Get Character Name by ID
[MUD Explorer](https://explorer.mud.dev/pyrope/worlds/0xcdb380e0cd3949caf70c45c67079f2e27a77fc47/explore?tableId=0x746265766566726f6e74696572000000456e746974795265636f72644d657461&query=SELECT%2520%2522smartObjectId%2522%252C%2520%2522name%2522%252C%2520%2522dappURL%2522%252C%2520%2522description%2522%2520FROM%2520%2522evefrontier__EntityRecordMeta%2522%2520LIMIT%25201000%2520OFFSET%25200%253B&page=0&pageSize=100)
Fetch character `name` by `characterId` using the `EntityRecordMeta` table.

### Get Tribe ID by Character ID
[MUD Explorer](https://explorer.mud.dev/pyrope/worlds/0xcdb380e0cd3949caf70c45c67079f2e27a77fc47/explore?tableId=0x746265766566726f6e7469657200000043686172616374657273000000000000&query=SELECT%2520%2522smartObjectId%2522%252C%2520%2522exists%2522%252C%2520%2522tribeId%2522%252C%2520%2522createdAt%2522%2520FROM%2520%2522evefrontier__Characters%2522%2520LIMIT%2520100%2520OFFSET%25200%253B&page=0&pageSize=100&filter=)
Fetch what tribe  (`tribeId`) a character belongs to by `characterId` using the `Characters` table.

## Items

### Get Item `smartObjectId` (`itemid`) by `typeId`

You can use this utility to deterministically generate the on-chain `itemId` given the `typeId` (the ID used to denote items in the local DB in your game files):
```solidity
bytes32 constant hardcodedTenantId = 0xaef21cf96fe11f21f1942e49b070eeb260a15521b689c44fe6bc1ff8f021fee5;
ObjectIdLib.calculateObjectId(hardcodedTenantId, typeId);
```

## Ownership
### Smart Assembly
[MUD Explorer](https://explorer.mud.dev/pyrope/worlds/0xcdb380e0cd3949caf70c45c67079f2e27a77fc47/explore?tableId=0x746265766566726f6e746965720000004f776e65727368697042794f626a6563&query=SELECT+%22smartObjectId%22,+%22account%22+FROM+%22evefrontier__OwnershipByObjec%22+LIMIT+100+OFFSET+0;&page=0&pageSize=100)
Check if what `account`  owns a smart assembly (by `smartObjectId`) using the `OwnershipByObjec` table.

## Metadata
### Smart Assembly Type
[MUD Explorer](https://explorer.mud.dev/pyrope/worlds/0xcdb380e0cd3949caf70c45c67079f2e27a77fc47/explore?tableId=0x746265766566726f6e74696572000000536d617274417373656d626c79000000&query=SELECT%2520%2522smartObjectId%2522%252C%2520%2522assemblyType%2522%2520FROM%2520%2522evefrontier__SmartAssembly%2522%2520LIMIT%2520100%2520OFFSET%25200%253B&page=0&pageSize=100)
You can check what type a smart assembly is by it's `smartObjectId` using the `SmartAssembly` table. Current types are:
- `NWN` - Network Node.
- `manufacturing` - Manufacturing Deployable (Printers / refineries).
- `smart_hangar` - Hangars.
- `SSU` - Smart Storage Units.


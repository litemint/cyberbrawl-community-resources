# Cyberbrawl Shuffle Algorithm
Play Game: [https://cyberbrawl.io](https://cyberbrawl.io)  
Game Design: [https://kyungj.in/posts/blockchain-game-design-cyberbrawl-stellar/](https://kyungj.in/posts/blockchain-game-design-cyberbrawl-stellar/)  

## Rationale

**Game Balance:** Prevent deck configurations that could lead to infinite loops or game deadlocks, regardless of special card combinations.

**Strategic Depth:** Enable diverse playstyles (Aggro, Control, etc.) through flexible deck composition while maintaining competitive balance.

**Streamlined Gameplay:** Eliminate deck depletion concerns, allowing players to focus on strategy rather than card counting.

## Rotation

**Core Mechanic**: Cards cycle to the bottom of your deck after being played, creating a predictable rotation pattern.

**Forced Draw** (Victory Rush, Trojan): Inserts cards at the top of your deck without disrupting the existing order. These cards enter the normal rotation cycle after being drawn.

**Overclocking:** Permanently increases your hand size to 4 cards for the remainder of the game.

**Multi-Draw** (Fast Hands): Adds extra cards beyond your current hand limit (3 cards normally, 4 with Overclocking). Normal drawing resumes only when your hand drops to your hand limit or below.

**Special Case**: Boomerang re-enters rotation after a full cycle but doesn't retrigger its forced draw effect—it only activates once per play.

## Favorite Cards Probabilities Sheet

This spreadsheet calculates your odds of drawing specific cards based on your deck composition and favorite card selections.  
**Strategic Insight:** Understanding these probabilities helps you balance reliability on specific draws.

https://docs.google.com/spreadsheets/d/1ZhL15teEP4gGLqqUsluWM7OVdJNGaS-LFN61DVP7cn4/edit?usp=sharing

## Shuffle Pseudo code

```
// Initialize base card sets
Initialize BaseDamageSet  = [card_01_00005, card_01_00008, card_01_00010, card_01_00011]
Initialize BaseHealSet    = [card_01_00003, card_01_00006, card_01_00009]
Initialize BaseEnergySet  = [card_01_00001, card_01_00004, card_01_00007]

// Prepare player deck
Remove all passive cards from PlayerDeck
While PlayerDeck has less than 4 cards
    Add one card_01_00002 (Hellfire I) to PlayerDeck

// Shuffle all sets
Randomly shuffle BaseDamageSet
Randomly shuffle BaseHealSet
Randomly shuffle BaseEnergySet
Randomly shuffle PlayerDeck

// Trim to rotation limit
Trim PlayerDeck to 10 cards (max rotation)

// Apply special card replacements
If player has card_02_00060 (Brawler)
    Replace the first BaseHealSet card with card_02_00061 (Brawl)

If player has card_02_00031 (Primal Overload)
    Replace card_01_00001 (Overload I) with card_02_00031 (Primal Overload) in BaseEnergySet

If player has card_02_00050 (Hellfire spec)
    Replace BaseDamageSet with [card_02_00054, card_02_00054, card_02_00054, card_02_00054] (Primal Hellfire)

// Build final deck in rotation groups
Randomly shuffle (BaseDamageSet[0], BaseHealSet[0], BaseEnergySet[0], PlayerDeck[0], PlayerDeck[1])
Add the result to FinalDeck

Randomly shuffle (BaseDamageSet[1], BaseDamageSet[3], BaseEnergySet[1], PlayerDeck[2])
Add the result to FinalDeck

Randomly shuffle (BaseDamageSet[2], BaseHealSet[2], BaseEnergySet[2], PlayerDeck[3])
Add the result to FinalDeck

If PlayerDeck length > 4
    Randomly shuffle (BaseDamageSet[0], BaseHealSet[1], BaseEnergySet[0], PlayerDeck[4])
    Add the result to FinalDeck

If PlayerDeck length > 5
    Randomly shuffle (BaseDamageSet[1], BaseDamageSet[3], BaseEnergySet[1], PlayerDeck[5])
    Add the result to FinalDeck

If PlayerDeck length > 6
    Randomly shuffle (BaseDamageSet[2], BaseHealSet[2], BaseEnergySet[2], PlayerDeck[6])
    Add the result to FinalDeck

If PlayerDeck length > 7
    Randomly shuffle (BaseDamageSet[0], BaseHealSet[1], BaseEnergySet[0], PlayerDeck[7])
    Add the result to FinalDeck

If PlayerDeck length > 8
    Randomly shuffle (BaseDamageSet[1], BaseDamageSet[3], BaseEnergySet[1], PlayerDeck[8])
    Add the result to FinalDeck

If PlayerDeck length > 9
    Randomly shuffle (BaseDamageSet[2], BaseHealSet[2], BaseEnergySet[2], PlayerDeck[9])
    Add the result to FinalDeck  
    
// Apply favorite card mechanic
Initialize FavoriteCardSet with all player favorited cards (starred), excluding passive cards
Randomly shuffle FavoriteCardSet

For each FavoriteCard in FavoriteCardSet
    If PlayerDeck has card_02_00056 (Chosen One) or getRandom(0,1) <= 0.75
       Move FavoriteCard to a random position within the first 3 cards in FinalDeck
       break

Filter FinalDeck to remove duplicates, allowing only card_02_00054 and all _01_ cards to remain
return FinalDeck
```

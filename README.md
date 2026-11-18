# Dead Lie Still
A wargame where defeat isn't the end.

This wargame was inspired by [Trolligarch's video](https://www.youtube.com/watch?v=MMjpej5Bcpo).

## General
The map is a hexagonal grid 13 tiles across (6 tiles from the centre to each edge, 127 tiles in total). Before the game starts, players choose starting locations without seeing the choices of others. Multiple players can occupy a tile. When the game starts, all players' locations are revealed and publicly visible for the rest of the game.

Players start with 1 blue token \(B\), 1 red token \(R\), and 3 lives \(L\). Players spend tokens on trading, moving, and attacking. Players also produce tokens.

Players who lose all of their lives become rogues. Rogues lose all of their blue tokens but keep their red tokens. Rogues no longer appear on the map, but they can still see it, and they can interact with players by trading and spying. Rogues cannot produce blue tokens, but they can still receive them through trades.

When a player is eliminated, all of their blue tokens go to their killer (see [Killer](#killer)).

The game takes place over a series of rounds lasting exactly 1 day. Players and rogues can select their actions at any time over the course of a round. At the end of a round (EoR), which occurs at a daily fixed time, all actions are performed in a fixed order (see [Order](#order)).

### Hidden Information
Player locations are public. Players and rogues always know their own lives (if applicable), token counts, and chosen actions. Everything else about other players and rogues is hidden: their lives, token counts, chosen actions, and action results. The only exceptions:
* Players who are eliminated learn who their killer is.
* Players know whether each of their attacks was successful (dealt damage).
* Players and rogues know whether each of their trades was successful (the target received the token).
* Players and rogues know who traded to them.
* Rogues can learn about players by spying.

### Winning and Points
The last player alive is declared the winner and the game ends.

At the end of each round, every player who is still a player (not a rogue) gains 1 point for every player who became a rogue that round. In other words, a player's score is the number of players eliminated before them. Players eliminated in the same round do not score points from each other. Rogues do not earn survival points.

At the end of the game, rogues gain 1 additional point for each blue token \(B\) they own.


## Actions

Players can choose any combination of the following actions (including multiple of the same action). Target refers to another player or rogue that is not yourself. All actions targeting players are limited by range: the target must be within 3 tiles of the acting player (a range 7 tiles across, centred on and including the acting player's tile). Players can interact with any rogue regardless of range.

| Action | Target | Cost | Effect |
| --- | --- | --- | --- |
| Attack | Player | 1 R | Target -1 L |
| Move | None | 1 R | You move to an adjacent tile of choice\*\* |
| Trade \(R\) | Player or Rogue | 1 R | Target +1 R |
| Trade \(B\) | Player or Rogue | 1 B | Target +1 B |
| Rebuild | None | 3 B | You +1 L* |

Each round, players also choose whether to produce a red or a blue token. If a player does not choose, they default to producing a blue token.

*Players' life counts are capped at 5 at the end of a round. This does not mean it is useless to rebuild when you are at 5 lives, see [Order](#order).

\*\*A player may Move several times in one round, paying 1 R per tile. Each Move steps from wherever the previous Move ended, in the order the player listed them.

Trade and attack actions can be selected as either priority or regular. See [Order](#order) for how that influences gameplay.

---

Rogues can choose any combination of the following actions (including multiple of the same action). Rogues are not subject to range limits, and can interact with any player or rogue.

| Action | Target | Cost | Effect |
| --- | --- | --- | --- |
| Trade \(R\) | Player or Rogue | 1 R | Target +1 R |
| Trade \(B\) | Player or Rogue | 1 B | Target +1 B |

Rogue trades can be selected as either priority or regular, the same as player trades, so rogues can fund players' attacks. Trades from players to rogues always happen after all attacks (see [Order](#order)), so rogues cannot relay tokens from one player to another within one round, only across multiple rounds.

Each round, rogues also choose between producing a red token and spying on one player. If a rogue does not choose, they produce a red token by default. Spying on a player gives the rogue information on that player's red token, blue token, and life counts.

Players become rogues at the end of a round, after all actions have been performed, so a new rogue cannot act as a rogue until the next round.

## Order

All actions and events in the game occur at the end of a round. This is the order in which they occur:

1. Token Generation
2. Attack (Priority)
3. Trade* (Priority)
4. Move
5. Trade* (Regular)
6. Attack (Regular)
7. Trade (Player to rogue)
8. Rebuild
9. Players with &le; 0 lives become rogues
10. Blue tokens go to killers
11. Players with > 5 lives are set to 5 lives
12. Surviving players gain points
13. Spy information is given

*Includes trades made by rogues, but not trades from players to rogues, which happen in step 7.

### Downed Players

During steps 2 to 7, a player whose lives are at 0 or below is **downed**. When a downed player's Attack, Trade, or Move would be performed, it is cancelled and its tokens are refunded. A downed player's Rebuild is still performed, and can bring them back above 0 lives before step 9.

Because downed players cannot attack, the player who makes the last successful attack of a round is always still alive afterwards, so at least one player always survives each round.

### Tiebreakers

Several trades or attacks can be queued for the same step, so tiebreakers decide the order in which they are performed. All tiebreaker values are taken immediately after Token Generation, before any other action occurs.

**Affordability.** Each player's actions of the same kind are numbered in the order the player listed them. A player's 1st attack is affordable if they have at least 1 red token, their 2nd attack if they have at least 2, and so on. Trades work the same way, counted separately for Trade \(R\) (against red tokens) and Trade \(B\) (against blue tokens). Trades to players and trades to rogues are numbered together. Unaffordable actions are still performed in their place in the order (and cancelled if the player cannot pay at that moment), but they are ordered after affordable actions and are not counted for any other tiebreaker.

Attacking: Given an action where A attacks B, the tiebreakers are considered in the following order, and the action that qualifies goes first:
1. The action is affordable
2. B has the fewest lives
3. A has the most affordable attacks targeted at B
4. A has the most affordable attacks
5. A has the most red tokens
6. Random chance

Trading: Given an action where A trades with B, the tiebreakers are considered in the following order, and the action that qualifies goes first:
1. The action is affordable
2. A has the most of the token being traded
3. B has the fewest of the token being traded
4. Random chance

All trades, including trades made by or to rogues, use the trading tiebreakers.

### Killer

The killer of an eliminated player receives all of that player's blue tokens. The killer is the acting player of the attack that brings the target down to 0 lives, counting lives gained through Rebuild. For example:
* X: 2 lives. Order: A attacks X, B attacks X, C attacks X, D attacks X, X rebuilds.
* X becomes a rogue. X had 3 lives in total \(including rebuild\), so C is the killer.

Only attackers who are still players at the end of the round can be killers. If the attacker found above becomes a rogue in the same round, the killer is the most recent earlier attacker of the target who is still a player. If there is no such attacker, the eliminated player's blue tokens are removed from the game.

### Clarifications

* Attacks and trades only work if the target is within range of the acting player at that moment.
* If an attack is out of range, the red tokens are still spent but no damage is dealt.
* Actions target players, not locations.
* An attack that takes the target's lives to a negative value is not refunded.
* If a trade is out of range, tokens are refunded.
* If an action's acting player does not have the tokens to perform the action at that moment, the action is cancelled and the tokens are refunded.
* If a rogue spies on a player who becomes a rogue that round, the rogue also learns who the killer was.
* Lives can go negative and go above 5 while the actions are performed. Tokens cannot go negative at any time.
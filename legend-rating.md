# The Legend Rating

How Cyberbrawl decides who is Legend #1.

The ladder is a climb through 25 ranks. Win a ranked battle, gain a star. Lose one, drop a star. That takes you to Legend at 120 stars and to a full Legend at 124, where stars freeze. From that point the question changes from "how far have you climbed" to "how strong are you", and that is what the rating answers.

## What it is

Every ranked battle you play, from your very first one, updates your rating. It measures your strength, and it orders the full Legends on the Season leaderboard: Legend #1 is the full Legend with the highest rating.

The system is Glicko-1, the rating used by chess servers and many competitive games. If you know Elo, Glicko is Elo with one extra idea: the system also tracks how sure it is about your number.

## Two numbers per player

- **Rating.** Your estimated strength. Everyone starts at 1400.
- **Deviation.** How uncertain the system is about that estimate. Everyone starts at 350, the maximum. It shrinks every time you play and settles at 50.

The deviation is what makes the system fair to new and returning players. A high deviation means "I do not know you yet", so results move your rating a lot. A low deviation means "I know you well", so each result is a small nudge.

## What one battle does

After each ranked battle the system compares what happened with what it expected.

1. It computes your **expected score**: the probability that you win, based on the gap between your rating and your opponent's. Equal ratings give 50%. A 200-point edge gives about 76%. A 400-point edge gives about 91%.
2. It takes the difference between the result (1 for a win, 0 for a loss) and that expectation. Beating a stronger opponent is a big positive surprise. Losing to a weaker one is a big negative surprise. Winning a battle you were expected to win barely registers.
3. It moves your rating by that surprise, scaled by your deviation. Then it lowers your deviation, because it has learned something.

Some real numbers from the formula, against an opponent rated 300 points above you:

| Your deviation | Win | Loss |
|---|---|---|
| 350, brand new | about +390 | about −70 |
| 50, settled | about +12 | about −2 |

Against an opponent rated the same as you, once settled: about +7 for a win, −7 for a loss.

The first-game swing is by design. The system has no idea how strong a new player is, so it lets the first results speak loudly. After about 30 battles the deviation reaches 50 and the swings settle into single digits.

## Time away

Within a season, deviation shrinks by playing and grows a little for every day away, so the system keeps an honest view of what it knows:

| Away for | Deviation on return |
|---|---|
| 0 days | 50 |
| 30 days | about 66 |
| 90 days | about 91 |
| a year | about 161 |

A returning player picks up where they left off. Their rating is unchanged, and their first battles back move it a bit more than usual, so a stronger or rustier player re-settles within a handful of games.

## The formula

For the curious, this is the exact update, one battle at a time. `r` and `rd` are your rating and deviation, the opponent has `r₀` and `rd₀`, and `s` is 1 for a win and 0 for a loss.

```
q  = ln(10) / 400
rd = min(350, sqrt(rd² + 8² × days idle))
g  = 1 / sqrt(1 + 3 q² rd₀² / π²)
E  = 1 / (1 + 10^(−g (r − r₀) / 400))
d² = 1 / (q² g² E (1 − E))
r  = r + q / (1/rd² + 1/d²) × g × (s − E)
rd = max(50, sqrt(1 / (1/rd² + 1/d²)))
```

`g` weighs the opponent's certainty: a result against someone the system knows well counts in full, a result against someone it barely knows counts a little less. Bots are known opponents with a deviation of 30, so results against them count almost in full.

## In short

- Stars take you to Legend. Rating orders the Legends.
- Everyone starts at 1400. Surprises move you, expected results barely do.
- The first 30 battles move you a lot. After that, a few points per game.
- Time away within a season makes your next games count more.

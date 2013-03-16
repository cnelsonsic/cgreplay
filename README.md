cgreplay
========

Replay Card Games

This braindead project proposes a Portable Card Game Notation (PCGN).
This format is inspired by Chess's Portable Game Notation.

A game file is standard JSON and consists of exactly one top level object
with two objects contained inside, "header" and "game".
Multiple games should be represented by multiple files.

The header object can contain such optional keys as:
* ``Event``: The name of the event that the game takes place at.
* ``Site``: The location of the event that the game takes place at.
* ``Date``: The date of the game
* ``Match``: The competitive match in a tournament
* ``Game``: The game of a match
* ``PlayerN``: The player number in the order of play.
* ``Result``: Which player or players won the game

The game object should contain they keys "player" and "move.
"Player" should have a digit indicating which player the move is for.
"Move" should have one of a number of simple phrases.

The syntax follows a "Source > Resource > Destination" format:
* Drawing a card looks like "library>Card Drawn>hand".
* Placing a card into play looks like "hand>Card Played>battlefield".
* Discarding a card looks like "hand>Card Discarded>graveyard".
* Activating a card's ability looks like "activate>Card To Activate, AbilityNumber". Ability numbers are one-indexed.
* Triggered abilities can be represented with "trigger>Card To Trigger, TriggeredAbilityNumber". Ability numbers are one-indexed.
* Changing players is similar: "turn>next"
* Changing phases is even more similar: "phase>next" or "phase>combat". These are based around the individual game and its implementation.

The source and destination depends on the game implementing the playback,
but should be the official names for those areas,
if in lowercase for consistency.

An example of such data:
```json
{
    "header": {
        "Event": "2038 Mars Pro Tour",
        "Site": "Mons Olympus, Mars",
        "Date": "2038.11.04",
        "Round": "29",
        "Game": "2",
        "Player1": "Dolan, D.",
        "Player2": "Gooby, G.",
        "Result": "1/2-1/2"
    },

    "game": [
        {"player": "1",
         "event": "library>Plains>hand"},
        },
        {"player": "1",
         "event": "hand>Plains>battlefield"},
        },
        {"player": "1",
         "event": "activate>Plains,1"},
        },
    ]
}
```

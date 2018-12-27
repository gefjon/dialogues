# `dialogues` - a scripting language

`dialogues` is a (currently theoretical) application-specific language for
writing scripts for interactive dialogues, for use primarily in text adventures
and visual novels.

```
Enter PHOEBE.
/*
```
 
A name (written in all caps) represents a semantic context within which to
evaluate functions & from which to produce data. New names are declared with
`Enter`.

```
*/
PHOEBE
What's your name?
/*
```

Normal `dialogue` syntax mimics [Fountain](https://fountain.io/), which I think
is elegant & syntactically well-defined. Note that not all Fountain files are
valid Scripts --- the compiler may try to interpret written text as
programmatic statements and will probably error. Plus, those scripts wouldn't
do anything, anyway, so what's the point?

```
*/
PLAYER (read-formatted-from stdin)
$GEFJON:name.

Rename PLAYER to GEFJON.
/*
```

`read-formatted-from` is `IO T.Text -> FormatString s -> ScriptReader s` & is
then applied to the item on the next line, which is compiled/parsed in a way
dependent on the type of the result of the call.

This section asks the player what their name is, with the default being
"Gefjon". It then updates the script, using the default name as a placeholder.

```
/*
Introduce hidden mood of PHOEBE called skepticism
    at 70
    of uint.
*/
```

Characters may have _moods_, which are variables of arbitrary types. They are
indexed with `-`, like `PHOEBE-sass`. This snippet introduces on,
initializes it, and annotates its type.

```
*/
GEFJON (read-choose-1-of 3)

(responds angry)
Who the hell are you, anyway? (increment PHOBEBE-skepticism 20)
PHOEBE
Like a ghost or some shit. Who knows these days?

(responds confused)
What's going on? What is all this? (decrement PHOEBE-skepticism 40)
PHOEBE
I know this must be kinda startling, but everything will be ok.

(responds indifferent)
...sup? (increment PHOEBE-skepticism 80)
PHOEBE
Look, if you don't want to talk to me you don't have to. I can wait.
/*
```

This snippet introduces the player with three choices, which are offered to the
player as `angry/confused/indifferent`. Each one alters PHOEBE's mood and then
responds with a quick line of dialogue.

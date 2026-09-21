# Folia Dialog Plugins

Paper **Dialog API** conversions of the chest GUIs in a set of Folia server
plugins. Each jar is the original plugin with its menus rewritten to use native
dialogs instead of chest inventories, built against Folia 1.21.11.

Download the jars from the [latest release](../../releases/latest).

## What changed

| Plugin | Screens converted | Notes |
| --- | --- | --- |
| Following | all | |
| Leaderboards | all | |
| BetterBounty | 2 | Search works on Folia now; it used a sign GUI, which Folia cannot show |
| Auction House | 13 | Framework-level conversion; 22 right-click actions became visible buttons |
| EconomyShopGUI-Premium | `/shop` | `/sellgui` stays a chest, see below. `/editshop` left as chests |
| DonutOrders | 9 of 10 | Deliver-items box stays a chest, see below |

## Two screens are still chests, on purpose

A dialog has no item slots, so any screen a player **drags items into** cannot
become one. There are two:

- EconomyShopGUI's `/sellgui` — you drop items in and it sells what you leave
- DonutOrders' `DeliverItemsGUI` — you drop items in to fulfil an order

Both are unchanged and still work as chests.

## Behaviour worth knowing about

- **Right-click actions are now buttons.** A dialog button has no right mouse
  button, so anything hidden behind a right-click — preview a shulker, jump to
  the last page, clear a search, sort backwards, sell instead of buy — is drawn
  as its own button. These were invisible affordances before.
- **Repaint timers are gone.** Auction House redrew every open chest once a
  second; re-showing a dialog that often fights the player. Screens redraw when
  something changes, and the refresh buttons still work.
- **Pages hold fewer items.** Each item costs a body row *and* a button, so a
  full 45-slot chest page would have come out as ~90 buttons.
- **Config compatibility.** Existing configs keep working untouched. Layout-only
  keys (rows, slots, filler materials) no longer apply; keys that still mean
  something are still read, and new keys have code-side defaults.

## Testing

Every jar was booted on a Folia 1.21.11 test server and driven through its
commands by a bot. All screens build and send with no server-side exceptions,
and the end-to-end command paths were exercised (listing an auction, placing a
bounty, creating orders, opening shop sections).

**Not verified:** the bot cannot click dialog buttons, so button behaviour —
navigation, buying, selling, collecting — needs a human pass.

## Licensing

Auction House, EconomyShopGUI-Premium and DonutOrders are paid plugins. These
are modified builds intended for the licence holder's own server.

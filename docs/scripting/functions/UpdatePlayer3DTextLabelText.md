---
title: UpdatePlayer3DTextLabelText
description: Updates a player 3D Text Label's text and color.
tags: ["player", "3dtextlabel"]
---

<VersionWarn version='SA-MP 0.3a' />

## Description

Updates a player 3D Text Label's text and color

| Name            | Description                                                   |
| --------------- | ------------------------------------------------------------- |
| playerid        | The ID of the player for which the 3D Text Label was created. |
| PlayerText3D:id | The 3D Text Label you want to update.                         |
| color           | The color the 3D Text Label should have from now on.          |
| text[]          | The new text which the 3D Text Label should have from now on. |

## Returns

This function does not return any specific values.

## Notes

:::warning

If text[] is empty, the server/clients next to the text might crash!

:::

## Related Functions

- [CreatePlayer3DTextLabel](CreatePlayer3DTextLabel): Create A 3D text label for one player.
- [DeletePlayer3DTextLabel](DeletePlayer3DTextLabel): Delete a player's 3D text label.
- [GetPlayer3DTextLabelText](GetPlayer3DTextLabelText): Gets the player's 3D text label text.
- [GetPlayer3DTextLabelColour](GetPlayer3DTextLabelColour): Gets the player's 3D text label colour.
- [Update3DTextLabelText](Update3DTextLabelText): Change the text of a 3D text label.

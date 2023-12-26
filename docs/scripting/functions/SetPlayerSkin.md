---
title: SetPlayerSkin
description: Seta Skin no playerid.
tags: ["player"]
---

## Descriçao

Seta a Skin no Player. A skin de um jogador é o modelo de seu personagem.

| Noame     | Descricao                                              |
| -------- | -------------------------------------------------------- |
| playerid | O ID do jogador cujo skin será definido.                 |
| skinid   | A [skin](../resources/skins) o jogador deve usar. |

## Returns

1: A funçao executada com Sucesso!

0: A função não foi executada. Isso significa que o Jogador especificado não existe.

Observe que o 'sucesso' é relatado mesmo quando o ID do skin é inválido (não 0-311 ou 74), mas o skin será definido como ID 0 (CJ).

## Exemplos

```c
public OnPlayerCommandText(playerid, cmdtext[])
{
    if (strcmp(cmdtext, "/bombeiro", true) == 0)
    {
        // Defina a skin do jogador para ID 277, que é um bombeiro.
        SetPlayerSkin(playerid, 277);
        return 1;
    }
    return 0;
}

SetPlayerSkinFix(playerid, skinid)
{
    if (!IsPlayerConnected(playerid))
    {
        return 0;
    }

    new
        Float:tmpPos[4],
        vehicleid = GetPlayerVehicleID(playerid),
        seatid = GetPlayerVehicleSeat(playerid);

    GetPlayerPos(playerid, tmpPos[0], tmpPos[1], tmpPos[2]);
    GetPlayerFacingAngle(playerid, tmpPos[3]);

    // Se o skin ID for inválido, menor que 0 ou maior que 311 ou igual a 74 (skin inválido), então não faz nada
    if (0 > skinid > 311 || skinid == 74)
    {
        return 0;
    }

    if (GetPlayerSpecialAction(playerid) == SPECIAL_ACTION_DUCK)
    {
        SetPlayerPos(playerid, tmpPos[0], tmpPos[1], tmpPos[2]);
        SetPlayerFacingAngle(playerid, tmpPos[3]);
        TogglePlayerControllable(playerid, true); // evitando qualquer congelamento - (opcional)
        return SetPlayerSkin(playerid, skinid);
    }
    else if (IsPlayerInAnyVehicle(playerid))
    {
        new
            tmp;

        RemovePlayerFromVehicle(playerid);
        SetPlayerPos(playerid, tmpPos[0], tmpPos[1], tmpPos[2]);
        SetPlayerFacingAngle(playerid, tmpPos[3]);
        TogglePlayerControllable(playerid, true); // evitando qualquer congelamento - importante! por causa de fazer animações de saída do veículo
        tmp = SetPlayerSkin(playerid, skinid);
        PutPlayerInVehicle(playerid, vehicleid, (seatid == 128) ? 0 : seatid);
        return tmp;
    }
    else
    {
        return SetPlayerSkin(playerid, skinid);
    }
}
```

## Notas

:::aviso

Bug(s) conhecido(s): Se a skin de um jogador for definida quando ele estiver agachado, em um veículo ou executando certas animações, ele ficará congelado ou apresentará falhas. Isso pode ser corrigido usando TogglePlayerControllable. Os jogadores podem ser detectados como agachados através de GetPlayerSpecialAction (SPECIAL_ACTION_DUCK). Outros jogadores ao redor do jogador podem bater se ele estiver em um veículo ou se estiver entrando/saindo de um veículo. Definir a pele de um jogador quando ele está morto pode derrubar os jogadores ao seu redor. Pausas sentadas em bicicletas.

:::

## =Funções Relacionadas

- [GetPlayerSkin](GetPlayerSkin): Getar a Skin Do Player
- [SetSpawnInfo](SetSpawnInfo): Defina a configuração de spawn para um jogador.

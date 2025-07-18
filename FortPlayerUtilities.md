
```verse
FortPlayerUtilities := module:

```
# Sends `InPlayer` back to the main game lobby.

```verse
    (InPlayer:player).SendToLobby<native><public>()<transacts>:void


```
    # Succeeds if `InAgent` is spectating the experience. Fails otherwise.

```verse
    (InAgent:agent).IsSpectator<native><public>()<transacts><decides>:void


```
    # Returns an `[]player`s currently spectating `InPlayer`.

```verse
    (InPlayer:player).GetPlayersSpectating<native><public>()<transacts>:[]player


```
    # Returns the agent a spectator is currently spectating, fails if the spectator isn't spectating or isn't spectating an agent.

```verse
    (InAgent:agent).GetSpectatedAgent<native><public>()<reads><decides>:agent


```
    # Returns an `[]agent`s currently spectating `InAgent`.

```verse
    (InAgent:agent).GetSpectators<native><public>()<transacts>:[]agent


```
    # Respawns the character for `InAgent` at the provided `RespawnPosition` and applies the yaw of `RespawnRotation`.

```verse
    (InAgent:agent).Respawn<native><public>(RespawnPosition:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, RespawnRotation:(/UnrealEngine.com/Temporary/SpatialMath:)rotation)<transacts>:void


```

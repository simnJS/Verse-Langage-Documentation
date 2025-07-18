# Playspaces Module

This module provides functionality for managing playspaces, which are nested containers that scope objects, style, gameplay rules, visuals, and more in Fortnite experiences.

## Fort Playspace Interface

```verse
Playspaces := module:
    # A nested container that scopes objects, style, gameplay rules, visuals, etc. All objects and players in an experience will belong to a fort_playspace. There is typically one `fort_playspace` for an entire experience, though this may change in the future as the platform evolves.
    # 
    # To access the `fort_playspace` for a `creative_device` use `creative_device.GetPlayspace`.
    fort_playspace<native><public> := interface<epic_internal>:
```

A nested container that scopes objects, style, gameplay rules, visuals, etc. All objects and players in an experience will belong to a fort_playspace. There is typically one fort_playspace for an entire experience, though this may change in the future as the platform evolves.

To access the fort_playspace for a creative_device, use `creative_device.GetPlayspace`.

### Player Management

#### GetPlayers
```verse
# Get all human `player`s that are in the current `fort_playspace`.
GetPlayers<public>()<transacts>:[]player
```

Gets all human players that are in the current fort_playspace.

#### PlayerAddedEvent
```verse
# Signaled when a human `player` joins the `fort_playspace`. Returns a subscribable with a payload of the`player` that entered the `fort_playspace`.
PlayerAddedEvent<public>():listenable(player)
```

Signaled when a human player joins the fort_playspace. Returns a subscribable with a payload of the player that entered the fort_playspace.

#### PlayerRemovedEvent
```verse
# Signaled when a human `player` leaves the `fort_playspace`. Returns a subscribable with a payload of the`player` that left the `fort_playspace`.
PlayerRemovedEvent<public>():listenable(player)
```

Signaled when a human player leaves the fort_playspace. Returns a subscribable with a payload of the player that left the fort_playspace.

### Team Management

#### GetTeamCollection
```verse
# Get the `fort_team_collection` for the current `fort_playspace`.
GetTeamCollection<public>()<transacts>:fort_team_collection
```

Gets the fort_team_collection for the current fort_playspace.

### Participant Management

#### GetParticipants
```verse
# Get all `agent`s that are participating in the current `fort_playspace` experience. Participants might be human players (of `player` type) or AI-controlled characters (of `agent` type) that are registered and affecting the participant's count.
GetParticipants<public>()<transacts>:[]agent
```

Gets all agents that are participating in the current fort_playspace experience. Participants might be human players (of player type) or AI-controlled characters (of agent type) that are registered and affecting the participant's count.

#### ParticipantAddedEvent
```verse
# Signaled when a participant `agent` joins the `fort_playspace`. Returns a subscribable with a payload of the`agent` that entered the `fort_playspace`.
ParticipantAddedEvent<public>():listenable(agent)
```

Signaled when a participant agent joins the fort_playspace. Returns a subscribable with a payload of the agent that entered the fort_playspace.

#### ParticipantRemovedEvent
```verse
# Signaled when a participant `agent` leaves the `fort_playspace`. Returns a subscribable with a payload of the`agent` that left the `fort_playspace`.
ParticipantRemovedEvent<public>():listenable(agent)
```

Signaled when a participant agent leaves the fort_playspace. Returns a subscribable with a payload of the agent that left the fort_playspace.

## Entity Playspace Access

### GetPlayspaceForEntity
```verse
# Returns an associated `fort_playspace` for this entity.  * Fails if this entity is not in the scene, and therefore not associated with a playspace.
(InEntity:entity).GetPlayspaceForEntity<native><public>()<transacts><decides>:fort_playspace
```

Returns an associated fort_playspace for this entity. Fails if this entity is not in the scene, and therefore not associated with a playspace.

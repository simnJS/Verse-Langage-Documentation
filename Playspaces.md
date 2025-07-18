
```verse
Playspaces := module:

```
# A nested container that scopes objects, style, gameplay rules, visuals, etc. All objects and players in an experience will belong to a fort_playspace. There is typically one `fort_playspace` for an entire experience, though this may change in the future as the platform evolves.
    # 
    # To access the `fort_playspace` for a `creative_device` use `creative_device.GetPlayspace`.

```verse
    fort_playspace<native><public> := interface<epic_internal>:

```
        # Get all human `player`s that are in the current `fort_playspace`.

```verse
        GetPlayers<public>()<transacts>:[]player


```
        # Get the `fort_team_collection` for the current `fort_playspace`.

```verse
        GetTeamCollection<public>()<transacts>:fort_team_collection


```
        # Signaled when a human `player` joins the `fort_playspace`. Returns a subscribable with a payload of the`player` that entered the `fort_playspace`.

```verse
        PlayerAddedEvent<public>():listenable(player)


```
        # Signaled when a human `player` leaves the `fort_playspace`. Returns a subscribable with a payload of the`player` that left the `fort_playspace`.

```verse
        PlayerRemovedEvent<public>():listenable(player)


```
        # Get all `agent`s that are participating in the current `fort_playspace` experience. Participants might be human players (of `player` type) or AI-controlled characters (of `agent` type) that are registered and affecting the participant's count.

```verse
        GetParticipants<public>()<transacts>:[]agent


```
        # Signaled when a participant `agent` joins the `fort_playspace`. Returns a subscribable with a payload of the`agent` that entered the `fort_playspace`.

```verse
        ParticipantAddedEvent<public>():listenable(agent)


```
        # Signaled when a participant `agent` leaves the `fort_playspace`. Returns a subscribable with a payload of the`agent` that left the `fort_playspace`.

```verse
        ParticipantRemovedEvent<public>():listenable(agent)


```
    # Returns an associated `fort_playspace` for this entity.  * Fails if this entity is not in the scene, and therefore not associated with a playspace.

```verse
    (InEntity:entity).GetPlayspaceForEntity<native><public>()<transacts><decides>:fort_playspace


```

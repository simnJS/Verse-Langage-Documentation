
```verse
Teams := module:

```
# A generic set of team attitudes. Use this enum to model relationship behavior between your experience's agents/teams.

```verse
    team_attitude<native><public> := enum:

```
        # Agents/teams are friends. In Fortnite games two `agent`s on the same `team` are `friendly`.

```verse
        Friendly

```
        # Agents/teams are neutral. In Fortnite games items and AI not belonging to a `friendly` or `hostile` team are `neutral`.

```verse
        Neutral

```
        # Agents/teams are hostile. In fortnite games two `agent`s on opposing `team`s are `hostile`.

```verse
        Hostile


```
    # Collection used to manage `team`s and `agent`s on those teams.
    # Use `fort_playspace.GetTeamCollection()` to get the `team_collection` for the active experience.

```verse
    fort_team_collection<native><public> := interface<epic_internal>:

```
        # Returns an array of all the `team`s known to this `fort_team_collection`

```verse
        GetTeams<public>()<transacts>:[]team


```
        # Adds `InAgent` to `InTeam`.
        # Fails if `InTeam` is not part of the `fort_team_collection`.

```verse
        AddToTeam<public>(InAgent:agent, InTeam:team)<transacts><decides>:void


```
        # Succeeds if `InAgent` is on `InTeam`.
        # Fails if:
        #  * `InAgent` is not on `InTeam`.
        #  * `InTeam` is not part of the `fort_team_collection`.

```verse
        IsOnTeam<public>(InAgent:agent, InTeam:team)<transacts><decides>:void


```
        # Returns an array of all `agent`s on `InTeam`.
        # Fails if `InTeam` is not part of the `fort_team_collection`.

```verse
        GetAgents<public>(InTeam:team)<transacts><decides>:[]agent


```
        # Get the `team` that `InAgent` is on.
        # Fails if `InAgent` is not on a team in this `fort_team_collection`.

```verse
        GetTeam<public>(InAgent:agent)<transacts><decides>:team


```
        # Returns the `team_attitude` between `Team1` and `Team2`.
        # Fails if:
        #  * `Team1` is not in this `fort_team_collection`.
        #  * `Team2` is not in this `fort_team_collection`.

```verse
        GetTeamAttitude<public>(Team1:team, Team2:team)<transacts><decides>:team_attitude


```
        # Returns the `team_attitude` between `Agent1` and `Agent2`.
        # Fails if:
        #  * `Agent1` is not on a team in this `fort_team_collection`.
        #  * `Agent2` is not on a team in this `fort_team_collection`.

```verse
        GetTeamAttitude<public>(Agent1:agent, Agent2:agent)<transacts><decides>:team_attitude


```

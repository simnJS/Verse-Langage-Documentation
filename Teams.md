# Teams Module

This module provides team management functionality for organizing agents and managing team relationships in Fortnite experiences.

## Team Attitude Enum

```verse
Teams := module:
    # A generic set of team attitudes. Use this enum to model relationship behavior between your experience's agents/teams.
    team_attitude<native><public> := enum:
```

A generic set of team attitudes used to model relationship behavior between agents and teams.

### Attitude Types

#### Friendly
```verse
# Agents/teams are friends. In Fortnite games two `agent`s on the same `team` are `friendly`.
Friendly
```

Agents/teams are friends. In Fortnite games, two agents on the same team are considered friendly.

#### Neutral
```verse
# Agents/teams are neutral. In Fortnite games items and AI not belonging to a `friendly` or `hostile` team are `neutral`.
Neutral
```

Agents/teams are neutral. In Fortnite games, items and AI not belonging to a friendly or hostile team are neutral.

#### Hostile
```verse
# Agents/teams are hostile. In fortnite games two `agent`s on opposing `team`s are `hostile`.
Hostile
```

Agents/teams are hostile. In Fortnite games, two agents on opposing teams are hostile.

## Team Collection Interface

```verse
# Collection used to manage `team`s and `agent`s on those teams.
# Use `fort_playspace.GetTeamCollection()` to get the `team_collection` for the active experience.
fort_team_collection<native><public> := interface<epic_internal>:
```

Collection used to manage teams and agents on those teams. Use `fort_playspace.GetTeamCollection()` to get the team collection for the active experience.

### Team Management

#### GetTeams
```verse
# Returns an array of all the `team`s known to this `fort_team_collection`
GetTeams<public>()<transacts>:[]team
```

Returns an array of all teams known to this team collection.

#### AddToTeam
```verse
# Adds `InAgent` to `InTeam`.
# Fails if `InTeam` is not part of the `fort_team_collection`.
AddToTeam<public>(InAgent:agent, InTeam:team)<transacts><decides>:void
```

Adds an agent to a team. Fails if the team is not part of the team collection.

#### IsOnTeam
```verse
# Succeeds if `InAgent` is on `InTeam`.
# Fails if:
#  * `InAgent` is not on `InTeam`.
#  * `InTeam` is not part of the `fort_team_collection`.
IsOnTeam<public>(InAgent:agent, InTeam:team)<transacts><decides>:void
```

Succeeds if the agent is on the specified team. Fails if:
- The agent is not on the team
- The team is not part of the team collection

#### GetAgents
```verse
# Returns an array of all `agent`s on `InTeam`.
# Fails if `InTeam` is not part of the `fort_team_collection`.
GetAgents<public>(InTeam:team)<transacts><decides>:[]agent
```

Returns an array of all agents on the specified team. Fails if the team is not part of the team collection.

#### GetTeam
```verse
# Get the `team` that `InAgent` is on.
# Fails if `InAgent` is not on a team in this `fort_team_collection`.
GetTeam<public>(InAgent:agent)<transacts><decides>:team
```

Gets the team that the agent is on. Fails if the agent is not on a team in this team collection.

### Attitude Queries

#### GetTeamAttitude (Team vs Team)
```verse
# Returns the `team_attitude` between `Team1` and `Team2`.
# Fails if:
#  * `Team1` is not in this `fort_team_collection`.
#  * `Team2` is not in this `fort_team_collection`.
GetTeamAttitude<public>(Team1:team, Team2:team)<transacts><decides>:team_attitude
```

Returns the team attitude between two teams. Fails if either team is not in this team collection.

#### GetTeamAttitude (Agent vs Agent)
```verse
# Returns the `team_attitude` between `Agent1` and `Agent2`.
# Fails if:
#  * `Agent1` is not on a team in this `fort_team_collection`.
#  * `Agent2` is not on a team in this `fort_team_collection`.
GetTeamAttitude<public>(Agent1:agent, Agent2:agent)<transacts><decides>:team_attitude
```

Returns the team attitude between two agents. Fails if either agent is not on a team in this team collection.

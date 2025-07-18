# AI Module

This module provides comprehensive AI functionality for Fortnite experiences, including NPC actions, perception, navigation, and focus management.

## AI Action Result Enum

```verse
AI := module:
@experimental
    # Result of an AI action
    ai_action_result<native><public> := enum<open>:
```

Result of an AI action:
- **Success**: The action has been successfully executed
- **Failure**: The action has failed during its execution
- **Canceled**: The action has been canceled before completion
- **Disallowed**: The action was not allowed to start

## Focus Interface

```verse
focus_interface<native><public> := interface<epic_internal>:
```

Interface for managing character focus and attention.

### Focus Methods

#### MaintainFocus (Location)
```verse
# Look At specified location. Will never complete unless interrupted.
MaintainFocus<public>(Location:(/UnrealEngine.com/Temporary/SpatialMath:)vector3)<suspends>:void
```

Look at specified location. Will never complete unless interrupted.

#### MaintainFocus (Agent)
```verse
# Look At specified Agent. Will never complete unless interrupted.
MaintainFocus<public>(Agent:agent)<suspends>:void
```

Look at specified agent. Will never complete unless interrupted.

### Focus Interface Access

```verse
# Get the focus_interface interface for the specified character.
(InCharacter:fort_character).GetFocusInterface<native><public>()<transacts><decides>:focus_interface
```

Gets the focus_interface for the specified character.

## Fort Guard Actions Interface

```verse
@experimental
# Fortnite Guards AI actions management
fort_guard_actions<native><public> := interface<epic_internal>(fort_npc_actions, fort_leashable):
```

Fortnite Guards AI actions management interface.

### Movement Actions

#### RoamAround
```verse
# Roam around the current position. Use the fort_leashable_component to specify the radius, else will roam anywhere.
RoamAround<public>(?MovementType:movement_type = external {})<suspends>:navigation_result
```

Roam around the current position. Use the fort_leashable_component to specify the radius, else will roam anywhere.

#### MoveInRangeToAttack
```verse
# Move in range to attack the current target
MoveInRangeToAttack<public>()<suspends>:ai_action_result
```

Move in range to attack the current target.

### Interaction Actions

#### PlayRandomEmote
```verse
# Play a random emote from the character emotes bank
PlayRandomEmote<public>()<suspends>:ai_action_result
```

Play a random emote from the character emotes bank.

#### Revive
```verse
# Revive the specified target
Revive<public>(Target:agent)<suspends>:ai_action_result
```

Revive the specified target.

#### Attack
```verse
# Attack the target
Attack<public>(Target:fort_target_info)<suspends>:ai_action_result
```

Attack the target.

### Fort Guard Actions Access

```verse
@experimental
# Get the current fort_guard_actions interface for the specified character.
(InCharacter:fort_character).GetFortGuardActions<native><public>()<transacts><decides>:fort_guard_actions
```

Gets the current fort_guard_actions interface for the specified character.

## Fort Guard Perception Interface

```verse
@experimental
# Fortnite NPC perception management
fort_guard_perception<native><public> := interface<epic_internal>(fort_npc_perception):
```

Fortnite NPC perception management interface.

### Target Information

#### GetCurrentTargetInfo
```verse
@experimental
# Get information about the current target.
GetCurrentTargetInfo<public>()<reads><decides>:fort_target_info
```

Gets information about the current target.

#### GetAlertLevel (Guard)
```verse
@experimental
# Get the current alert level of the guard.
GetAlertLevel<public>()<reads>:fort_guard_alert_level
```

Gets the current alert level of the guard.

#### GetAlertLevel (Target)
```verse
@experimental
# Get the current alert level of a target for the guard.
GetAlertLevel<public>(Target:entity)<reads><decides>:fort_guard_alert_level
```

Gets the current alert level of a target for the guard.

### Events

#### AlertLevelChangedEvent
```verse
@experimental
# Event when the alert level of the guard has changed.
AlertLevelChangedEvent<public>:listenable(fort_guard_alert_level)
```

Event when the alert level of the guard has changed.

#### CurrentTargetChangedEvent
```verse
@experimental
# Event when the current target has changed.
CurrentTargetChangedEvent<public>:listenable(fort_target_info)
```

Event when the current target has changed.

### Fort Guard Perception Access

```verse
@experimental
# Get the current fort_guard_perception interface for the specified character.
(InCharacter:fort_character).GetFortGuardPerception<native><public>()<transacts><decides>:fort_guard_perception
```

Gets the current fort_guard_perception interface for the specified character.

## Fort Leashable Interface

```verse
fort_leashable<native><public> := interface<epic_internal>:
```

Interface for managing character leash behavior.

### Leash Management

#### SetLeashPosition
```verse
# Set custom leash position.
#  'InnerRadius' ranges from 0.0 to 20000.0 (in centimeters).
#  'OuterRadius' ranges from 0.0 to 20000.0 (in centimeters) and no less than 'InnerRadius'.
SetLeashPosition<public>(Location:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, InnerRadius:float, OuterRadius:float):void
```

Set custom leash position:
- **InnerRadius**: Ranges from 0.0 to 20000.0 (in centimeters)
- **OuterRadius**: Ranges from 0.0 to 20000.0 (in centimeters) and no less than InnerRadius

#### SetLeashAgent
```verse
# Set the agent to be the new center of the leash.
#  'InnerRadius' ranges from 0.0 to 20000.0 (in centimeters).
#  'OuterRadius' ranges from 0.0 to 20000.0 (in centimeters) and no less than 'InnerRadius'.
SetLeashAgent<public>(Agent:agent, InnerRadius:float, OuterRadius:float):void
```

Set the agent to be the new center of the leash:
- **InnerRadius**: Ranges from 0.0 to 20000.0 (in centimeters)
- **OuterRadius**: Ranges from 0.0 to 20000.0 (in centimeters) and no less than InnerRadius

#### ClearLeash
```verse
# Removes the current leash.
ClearLeash<public>():void
```

Removes the current leash.

### Fort Leashable Access

```verse
# Get the current fort_leashable interface for the specified character.
(InCharacter:fort_character).GetFortLeashable<native><public>()<transacts><decides>:fort_leashable
```

Gets the current fort_leashable interface for the specified character.

## Fort NPC Actions Interface

```verse
@experimental
# Fortnite NPC AI actions management
fort_npc_actions<native><public> := interface<epic_internal>(navigatable, focus_interface):
```

Fortnite NPC AI actions management interface.

### Fort NPC Actions Access

```verse
@experimental
# Get the current fort_npc_actions interface for the specified character.
(InCharacter:fort_character).GetFortNPCActions<native><public>()<transacts><decides>:fort_npc_actions
```

Gets the current fort_npc_actions interface for the specified character.

## Fort NPC Perception Interface

```verse
@experimental
# Fortnite NPC perception management
fort_npc_perception<native><public> := interface<epic_internal>:
```

Fortnite NPC perception management interface.

### Target Information

#### GetLastKnownPosition
```verse
@experimental
# Get the last known position of a target.
GetLastKnownPosition<public>(Target:entity)<reads><decides>:(/UnrealEngine.com/Temporary/SpatialMath:)vector3
```

Gets the last known position of a target.

### Events

#### TargetAddedEvent
```verse
@experimental
# Event when a target is added.
TargetAddedEvent<public>:listenable(fort_target_info)
```

Event when a target is added.

#### TargetInfoUpdatedEvent
```verse
@experimental
# Event when the info about a target has been updated.
TargetInfoUpdatedEvent<public>:listenable(fort_target_info)
```

Event when the info about a target has been updated.

#### TargetRemovedEvent
```verse
@experimental
# Event when a target was removed.
TargetRemovedEvent<public>:listenable(entity)
```

Event when a target was removed.

#### TargetSeenEvent
```verse
@experimental
# Event when a target is seen. Sight sense must be active.
TargetSeenEvent<public>:listenable(fort_target_info)
```

Event when a target is seen. Sight sense must be active.

#### TargetHeardEvent
```verse
@experimental
# Event when a target is heard. Hearing sense must be active.
TargetHeardEvent<public>:listenable(fort_target_info)
```

Event when a target is heard. Hearing sense must be active.

#### TargetTouchedEvent
```verse
@experimental
# Event when a target is touched. Touch sense must be active.
TargetTouchedEvent<public>:listenable(fort_target_info)
```

Event when a target is touched. Touch sense must be active.

### Properties

#### DetectedTargets
```verse
@experimental
# Information about all detected targets.
var<epic_internal> DetectedTargets<public>:[]fort_target_info
```

Information about all detected targets.

### Fort NPC Perception Access

```verse
@experimental
# Get the current fort_npc_perception interface for the specified character.
(InCharacter:fort_character).GetFortNPCPerception<native><public>()<transacts><decides>:fort_npc_perception
```

Gets the current fort_npc_perception interface for the specified character.

## Navigation Target Class

```verse
navigation_target<native><public> := class<epic_internal>:
```

Class for representing navigation targets.

### Navigation Target Creation

#### MakeNavigationTarget (Position)
```verse
# Generate a navigation_target from any position
MakeNavigationTarget<public>(Position:(/UnrealEngine.com/Temporary/SpatialMath:)vector3):navigation_target = external {}
```

Generate a navigation_target from any position.

#### MakeNavigationTarget (Agent)
```verse
# Generate a navigation_target from an agent
MakeNavigationTarget<native><public>(Target:agent):navigation_target
```

Generate a navigation_target from an agent.

#### MakeNavigationTarget (Entity)
```verse
@experimental
# Generate a navigation_target from an entity
MakeNavigationTarget<native><public>(Entity:entity):navigation_target
```

Generate a navigation_target from an entity.

## Navigation Result Enum

```verse
# Result of a navigation request
navigation_result<native><public> := enum:
```

Result of a navigation request:
- **Reached**: The destination has been reached
- **PartiallyReached**: The destination has been partially reached (AllowPartialPath was used)
- **Interrupted**: Navigation has been interrupted before completion
- **Blocked**: The navigating agent is blocked
- **Unreachable**: The destination cannot be reached

## Movement Type Class

```verse
movement_type<native><public> := class<concrete><final><computes><epic_internal>:
```

Class for defining movement types.

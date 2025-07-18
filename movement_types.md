# Movement Types Module

This module provides movement type definitions and navigation functionality for Fortnite characters and NPCs.

## Movement Type Constants

```verse
movement_types := module:
Walking<public>:movement_type = external {}
Running<public>:movement_type = external {}
```

Predefined movement types:
- **Walking**: Standard walking movement
- **Running**: Fast running movement

## Navigatable Interface

```verse
navigatable<native><public> := interface<epic_internal>:
```

Interface for character navigation and movement control.

### Navigation Methods

#### GetCurrentDestination
```verse
# Return the current destination of the character
GetCurrentDestination<public>()<transacts><decides>:(/UnrealEngine.com/Temporary/SpatialMath:)vector3
```

Returns the current destination of the character.

#### NavigateTo
```verse
# Navigate toward the specified target
NavigateTo<public>(Target:navigation_target, ?MovementType:movement_type = external {}, ?ReachRadius:float = external {}, ?AllowPartialPath:logic = external {})<suspends>:navigation_result
```

Navigate toward the specified target with optional parameters:
- **Target**: The navigation target to move toward
- **MovementType**: Type of movement to use (optional)
- **ReachRadius**: Radius within which the target is considered reached (optional)
- **AllowPartialPath**: Whether to allow partial path completion (optional)

#### StopNavigation
```verse
# Stop navigation
StopNavigation<public>():void
```

Stops the current navigation.

#### Wait
```verse
# Wait for a specific duration
Wait<public>(?Duration:float = external {})<suspends>:void
```

Wait for a specific duration. If no duration is specified, waits indefinitely.

#### SetMovementSpeedMultiplier
```verse
# Apply a multiplier on the movement speed (Multiplier is clamped between 0.5 and 2)
SetMovementSpeedMultiplier<public>(Multiplier:float):void
```

Apply a multiplier on the movement speed. Multiplier is clamped between 0.5 and 2.

### Navigatable Interface Access

```verse
# Get the navigatable interface for the specified character
(InCharacter:fort_character).GetNavigatable<native><public>()<transacts><decides>:navigatable
```

Gets the navigatable interface for the specified character.

## NPC Behavior Base Class

```verse
# Inherit from this to create a custom NPC behavior.
# The npc_behavior can be defined for a character in a CharacterDefinition asset, or in a npc_spawner_device.
npc_behavior<native><public> := class<abstract>:
```

Base class for creating custom NPC behaviors. Can be defined for a character in a CharacterDefinition asset or in a npc_spawner_device.

### Lifecycle Methods

#### OnBegin
```verse
# This function is called when the NPC is added to the simulation.
OnBegin<native_callable><public>()<suspends>:void = external {}
```

This function is called when the NPC is added to the simulation.

#### OnEnd
```verse
# This function is called when the NPC is removed from the simulation.
OnEnd<native_callable><public>():void = external {}
```

This function is called when the NPC is removed from the simulation.

### Utility Methods

#### GetAgent
```verse
# Returns the agent associated with this behavior.
GetAgent<native><public>()<transacts><decides>:agent
```

Returns the agent associated with this behavior.

### NPC Behavior Access

```verse
# Returns the `npc_behavior` for `InAgent`.
(InAgent:agent).GetNPCBehavior<native><public>()<transacts><decides>:npc_behavior
```

Returns the npc_behavior for the specified agent.

```verse
@experimental
# Returns the `entity` for `InNPCBehavior`.
(InNPCBehavior:npc_behavior).GetEntity<native><public>()<reads><decides>:entity
```

Returns the entity for the specified NPC behavior.

## Fort Guard Alert Level Enum

```verse
@experimental
# The different alert levels of a guard.
fort_guard_alert_level<native><public> := enum:
```

The different alert levels of a guard:
- **Unaware**: The guard has not detected any hostile target
- **Suspicious**: The guard has seen a hostile target but hasn't identified it yet
- **LostTarget**: The guard has identified a hostile target but can't see it any more
- **Alerted**: The guard has identified a hostile target

## Fort Target Info Class

```verse
@experimental
# Information about a perceived target.
fort_target_info<native><public> := class<epic_internal>:
```

Information about a perceived target.

### Properties

#### Target
```verse
@experimental
# The source of the detection stimuli.
Target<native><public>:entity
```

The source of the detection stimuli.

#### HasLineOfSight
```verse
@experimental
# True if the target can be seen.
HasLineOfSight<native><public>:logic
```

True if the target can be seen.

#### Attitude
```verse
@experimental
# Attitude toward this target.
Attitude<native><public>:team_attitude
```

Attitude toward this target.

### Navigation Target Creation

```verse
@experimental
# Create a `navigation_target` from a `fort_target_info`.
MakeNavigationTarget<native><public>(TargetInfo:fort_target_info):navigation_target
```

Create a navigation_target from a fort_target_info.

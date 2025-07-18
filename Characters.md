# Characters Module

This module provides comprehensive character functionality for Fortnite experiences, including character state management, movement, and interactions.

## Fort Character Interface

```verse
Characters := module:
    # Main API implemented by Fortnite characters.
    fort_character<native><public> := interface<unique><epic_internal>(positional, healable, healthful, damageable, shieldable, game_action_instigator, game_action_causer):
```

Main API implemented by Fortnite characters.

### Character Information

#### GetAgent
```verse
# Returns the agent associated with this `fort_character`. Use this when interacting with APIs that require an `agent` reference.
GetAgent<public>()<transacts><decides>:agent
```

Returns the agent associated with this fort_character. Use this when interacting with APIs that require an agent reference.

#### GetViewRotation
```verse
# Returns the rotation where this `fort_character` is looking or aiming at.
GetViewRotation<public>()<transacts>:(/UnrealEngine.com/Temporary/SpatialMath:)rotation
```

Returns the rotation where this fort_character is looking or aiming at.

#### GetViewLocation
```verse
# Returns the location where this `fort_character` is looking or aiming from.
GetViewLocation<public>()<transacts>:(/UnrealEngine.com/Temporary/SpatialMath:)vector3
```

Returns the location where this fort_character is looking or aiming from.

### Character State Checks

#### IsActive
```verse
# Succeeds if this `fort_character` is in the world and has not been eliminated. Most fort_character actions will silently fail if this fails. Please test IsActive if you want to handle these failure cases rather than allow them to silently fail.
IsActive<public>()<transacts><decides>:void
```

Succeeds if this fort_character is in the world and has not been eliminated. Most fort_character actions will silently fail if this fails. Test IsActive if you want to handle these failure cases rather than allow them to silently fail.

#### IsDownButNotOut
```verse
# Succeeds if this `fort_character` is in the 'Down But Not Out' state. In this state the character is down but can still be revived by teammates for a period of time.
IsDownButNotOut<public>()<transacts><decides>:void
```

Succeeds if this fort_character is in the 'Down But Not Out' state. In this state the character is down but can still be revived by teammates for a period of time.

#### IsCrouching
```verse
# Succeeds if this `fort_character` is crouching.
IsCrouching<public>()<transacts><decides>:void
```

Succeeds if this fort_character is crouching.

### Environment State Checks

#### IsOnGround
```verse
# Succeeds if this `fort_character` is standing on the ground.
IsOnGround<public>()<transacts><decides>:void
```

Succeeds if this fort_character is standing on the ground.

#### IsInAir
```verse
# Succeeds if this `fort_character` is standing in the air.
IsInAir<public>()<transacts><decides>:void
```

Succeeds if this fort_character is standing in the air.

#### IsInWater
```verse
# Succeeds if this `fort_character` is inside water volume.
IsInWater<public>()<transacts><decides>:void
```

Succeeds if this fort_character is inside water volume.

### Movement State Checks

#### IsFalling
```verse
# Succeeds if this `fort_character` is in falling locomotion state.
IsFalling<public>()<transacts><decides>:void
```

Succeeds if this fort_character is in falling locomotion state.

#### IsGliding
```verse
# Succeeds if this `fort_character` is in gliding locomotion state.
IsGliding<public>()<transacts><decides>:void
```

Succeeds if this fort_character is in gliding locomotion state.

#### IsFlying
```verse
# Succeeds if this `fort_character` is in flying locomotion state.
IsFlying<public>()<transacts><decides>:void
```

Succeeds if this fort_character is in flying locomotion state.

### Character Control

#### PutInStasis
```verse
# Puts this `fort_character` into stasis, preventing certain types of movement specified by `Args`.
PutInStasis<public>(Args:stasis_args)<transacts>:void
```

Puts this fort_character into stasis, preventing certain types of movement specified by Args.

#### ReleaseFromStasis
```verse
# Release this `fort_character` from stasis.
ReleaseFromStasis<public>()<transacts>:void
```

Release this fort_character from stasis.

#### Show
```verse
# Sets this `fort_character` visibility to visible.
Show<public>():void
```

Sets this fort_character visibility to visible.

#### Hide
```verse
# Sets this `fort_character` visibility to invisible.
Hide<public>():void
```

Sets this fort_character visibility to invisible.

#### SetVulnerability
```verse
# Control if this `fort_character` can be damaged.
SetVulnerability<public>(Vulnerable:logic)<transacts>:void
```

Control if this fort_character can be damaged.

#### IsVulnerable
```verse
# Succeeds if this `fort_character` can be damaged. Fails if this `fort_character` cannot be damaged.
IsVulnerable<public>()<transacts><decides>:void
```

Succeeds if this fort_character can be damaged. Fails if this fort_character cannot be damaged.

#### TeleportTo
```verse
# Teleports this `fort_character` to the provided `Position` and applies the yaw and pitch of `Rotation`. Will fail if the `Position` specified is e.g. outside of the playspace or specifies a place where the character cannot fit.
TeleportTo<public>(Position:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, Rotation:(/UnrealEngine.com/Temporary/SpatialMath:)rotation)<transacts><decides>:void
```

Teleports this fort_character to the provided Position and applies the yaw and pitch of Rotation. Will fail if the Position specified is outside of the playspace or specifies a place where the character cannot fit.

### Events

#### EliminatedEvent
```verse
# Signaled when this `fort_character` is eliminated from the match.
EliminatedEvent<public>():listenable(elimination_result)
```

Signaled when this fort_character is eliminated from the match.

#### JumpedEvent
```verse
# Signaled when this `fort_character` jumps. Returns a listenable with a payload of this `fort_character`.
JumpedEvent<public>():listenable(fort_character)
```

Signaled when this fort_character jumps. Returns a listenable with a payload of this fort_character.

#### CrouchedEvent
```verse
# Signaled when this `fort_character` changes crouch state.
# Sends `tuple` payload:
#  - 0: the `fort_character` that changed crouch states.
#  - 1: `true` if the character is crouching. `false` if the character is not crouching.
CrouchedEvent<public>():listenable(tuple(fort_character, logic))
```

Signaled when this fort_character changes crouch state. Sends tuple payload:
- **0**: The fort_character that changed crouch states
- **1**: True if the character is crouching, false if the character is not crouching

#### SprintedEvent
```verse
# Signaled when this `fort_character` changes sprint state.
# Sends `tuple` payload:
#  - 0: the `fort_character` that changed sprint state.
#  - 1: `true` if the character is sprinting. `false` if the character stopped sprinting.
SprintedEvent<public>():listenable(tuple(fort_character, logic))
```

Signaled when this fort_character changes sprint state. Sends tuple payload:
- **0**: The fort_character that changed sprint state
- **1**: True if the character is sprinting, false if the character stopped sprinting

## Character Access Functions

### GetFortCharacter
```verse
# Returns the `fort_character` for `InAgent`. Fails if `InAgent` is not a `fort_character`.
(InAgent:agent).GetFortCharacter<native><public>()<transacts><decides>:fort_character
```

Returns the fort_character for InAgent. Fails if InAgent is not a fort_character.

### GetInstigator
```verse
# Returns a `game_action_instigator` interface for `InAgent`.
(InAgent:agent).GetInstigator<native><public>()<transacts>:game_action_instigator
```

Returns a game_action_instigator interface for InAgent.

### GetInstigatorAgent
```verse
# Returns the `agent` for `InInstigator`. Fails if `InInstigator` is not an `agent`.
(InInstigator:game_action_instigator).GetInstigatorAgent<native><public>()<transacts><decides>:agent
```

Returns the agent for InInstigator. Fails if InInstigator is not an agent.

## Stasis Args Structure

```verse
# Parameters for `fort_character.PutInStasis` function.
stasis_args<native><public> := struct:
```

Parameters for fort_character.PutInStasis function.

### Properties

#### AllowTurning
```verse
# Controls if `fort_character` can still turn while in stasis.
AllowTurning<native><public>:logic = external {}
```

Controls if fort_character can still turn while in stasis.

#### AllowFalling
```verse
# Controls if `fort_character` can still fall while in stasis.
AllowFalling<native><public>:logic = external {}
```

Controls if fort_character can still fall while in stasis.

#### AllowEmotes
```verse
# Controls if `fort_character` can still perform emotes while in stasis.
AllowEmotes<native><public>:logic = external {}
```

Controls if fort_character can still perform emotes while in stasis.

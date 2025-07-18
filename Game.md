# Game Module

This module provides comprehensive game mechanics functionality for Fortnite experiences, including elimination tracking, round management, health systems, damage, healing, and game action interfaces.

## Elimination Result Structure

```verse
Game := module:
    # Result data for `fort_character` elimination events.
    elimination_result<native><public> := struct<epic_internal>:
```

Result data for fort_character elimination events.

### Properties

#### EliminatedCharacter
```verse
# The `fort_character` eliminated from the match by `EliminatingCharacter`.
EliminatedCharacter<native><public>:fort_character
```

The fort_character eliminated from the match by EliminatingCharacter.

#### EliminatingCharacter
```verse
# `fort_character` that eliminated `EliminatedCharacter` from the match. `EliminatingCharacter` will be false when `EliminatedCharacter` was eliminated through non-character actions, such as environmental damage.
EliminatingCharacter<native><public>:?fort_character
```

Fort_character that eliminated EliminatedCharacter from the match. Will be false when EliminatedCharacter was eliminated through non-character actions, such as environmental damage.

## Fort Round Manager Interface

```verse
# This interface is implemented by the round manager living on the simulation entity.
fort_round_manager<native><public> := interface<epic_internal>:
```

This interface is implemented by the round manager living on the simulation entity.

### Round Management

#### SubscribeRoundStarted
```verse
# Subscribed callbacks will be invoked in two scenarios:
#  - When a new Fortnite round starts
#  - If a round is ongoing, your callback will be invoked immediately
# Upon the round ending, all callbacks will be canceled
SubscribeRoundStarted<public>(Callback:type {_()<suspends>:void}):cancelable
```

Subscribed callbacks will be invoked in two scenarios:
- When a new Fortnite round starts
- If a round is ongoing, your callback will be invoked immediately

Upon the round ending, all callbacks will be canceled.

#### SubscribeRoundEnded
```verse
# Subscribed callbacks will be invoked when a Fortnite round ends
SubscribeRoundEnded<public>(Callback:type {_():void}):cancelable
```

Subscribed callbacks will be invoked when a Fortnite round ends.

### Round Manager Access

```verse
# Returns the round manager from the simulation entity.
(InEntity:entity).GetFortRoundManager<public>()<transacts><decides>:fort_round_manager = external {}
```

Returns the round manager from the simulation entity.

## Positional Interface

```verse
# Implemented by objects to allow reading position information.
positional<native><public> := interface<epic_internal>:
```

Implemented by objects to allow reading position information.

### Position Methods

#### GetTransform
```verse
# Returns the transform of the object.
GetTransform<public>()<transacts>:(/UnrealEngine.com/Temporary/SpatialMath:)transform
```

Returns the transform of the object.

## Healthful Interface

```verse
# Implemented by Fortnite objects that have health state and can be eliminated.
healthful<native><public> := interface<epic_internal>:
```

Implemented by Fortnite objects that have health state and can be eliminated.

### Health Management

#### GetHealth
```verse
# Returns the health state of the object. This value will be between 0.0 and `GetMaxHealth`
GetHealth<public>()<transacts>:float
```

Returns the health state of the object. This value will be between 0.0 and GetMaxHealth.

#### SetHealth
```verse
# Sets the health state of the object to `Health`.
#  * Health state will be clamped between 1.0 and `GetMaxHealth`.
#  * Health state cannot be directly set to 0.0. To eliminate `healthful` objects use the `damageable.Damage` functions instead.
SetHealth<public>(Health:float)<transacts>:void
```

Sets the health state of the object to Health:
- Health state will be clamped between 1.0 and GetMaxHealth
- Health state cannot be directly set to 0.0. To eliminate healthful objects use the damageable.Damage functions instead.

#### GetMaxHealth
```verse
# Returns the maximum health of the object. This value will be between 1.0 and Inf.
GetMaxHealth<public>()<transacts>:float
```

Returns the maximum health of the object. This value will be between 1.0 and Inf.

#### SetMaxHealth
```verse
# Sets the maximum health state of the object.
#  * MaxHealth will be clamped between 1.0 and Inf.
#  * Current health state will be scaled up or down based on the scale difference between the old and new MaxHealth state.
SetMaxHealth<public>(MaxHealth:float)<transacts>:void
```

Sets the maximum health state of the object:
- MaxHealth will be clamped between 1.0 and Inf
- Current health state will be scaled up or down based on the scale difference between the old and new MaxHealth state.

## Shieldable Interface

```verse
# Implemented by Fortnite objects that have shields. A shield is a method of protection that can take incoming damage while leaving the health state unchanged.
shieldable<native><public> := interface<epic_internal>:
```

Implemented by Fortnite objects that have shields. A shield is a method of protection that can take incoming damage while leaving the health state unchanged.

### Shield Management

#### GetShield
```verse
# Returns the shield state of the object. This value will be between 0.0 and `MaxShield`
GetShield<public>()<transacts>:float
```

Returns the shield state of the object. This value will be between 0.0 and MaxShield.

#### SetShield
```verse
# Sets the shield state of the object.
#  * Shield state will be clamped between 0.0 and `MaxShield`.
SetShield<public>(Shield:float)<transacts>:void
```

Sets the shield state of the object. Shield state will be clamped between 0.0 and MaxShield.

#### GetMaxShield
```verse
# Returns the maximum shield state of the object. This value will be between 0.0 and Inf.
GetMaxShield<public>()<transacts>:float
```

Returns the maximum shield state of the object. This value will be between 0.0 and Inf.

#### SetMaxShield
```verse
# Sets the maximum shield state of the object.
#  * MaxShield will be clamped between 0.0 and Inf.
#  * Current shield state will be scaled up or down based on the scale difference between the old and new MaxShield state.
SetMaxShield<public>(MaxShield:float)<transacts>:void
```

Sets the maximum shield state of the object:
- MaxShield will be clamped between 0.0 and Inf
- Current shield state will be scaled up or down based on the scale difference between the old and new MaxShield state.

### Shield Events

#### DamagedShieldEvent
```verse
# Signaled when the shield is damaged.
DamagedShieldEvent<public>():listenable(damage_result)
```

Signaled when the shield is damaged.

#### HealedShieldEvent
```verse
# Signaled when the shield is healed.
HealedShieldEvent<public>():listenable(healing_result)
```

Signaled when the shield is healed.

## Damageable Interface

```verse
# Implemented by Fortnite objects that can be damaged.
damageable<native><public> := interface<epic_internal>:
```

Implemented by Fortnite objects that can be damaged.

### Damage Methods

#### Damage (Amount)
```verse
# Damage the `damageable` object anonymously by `Amount`. Setting `Amount` to less than 0 will cause no damage.
# Use `Damage(:damage_args):void` when damage is being applied from a known instigator and source.
Damage<public>(Amount:float):void
```

Damage the damageable object anonymously by Amount. Setting Amount to less than 0 will cause no damage. Use Damage(:damage_args):void when damage is being applied from a known instigator and source.

#### Damage (Args)
```verse
# Damage the `damageable` object by `Args.Amount`. Setting `Amount` to less than 0 will cause no damage.
Damage<public>(Args:damage_args):void
```

Damage the damageable object by Args.Amount. Setting Amount to less than 0 will cause no damage.

### Damage Events

#### DamagedEvent
```verse
# Signaled when damage is applied to the `damageable` object.
DamagedEvent<public>():listenable(damage_result)
```

Signaled when damage is applied to the damageable object.

## Healable Interface

```verse
# Implemented by Fortnite objects that can be healed.
healable<native><public> := interface<epic_internal>:
```

Implemented by Fortnite objects that can be healed.

### Healing Methods

#### Heal (Amount)
```verse
# Heal the `healable` object anonymously by `Amount`. Setting `Amount` to less than 0 will cause no healing.
# Use `Heal(:healing_args):void` when healing is being applied from a known instigator and source.
Heal<public>(Amount:float):void
```

Heal the healable object anonymously by Amount. Setting Amount to less than 0 will cause no healing. Use Heal(:healing_args):void when healing is being applied from a known instigator and source.

#### Heal (Args)
```verse
# Cause `Args.Amount` damage to the `damageable` object. Setting `Amount` to less than 0 will cause no damage.
Heal<public>(Args:healing_args):void
```

Cause Args.Amount healing to the healable object. Setting Amount to less than 0 will cause no healing.

### Healing Events

#### HealedEvent
```verse
# Signaled when healing is applied to the `healable` object.
HealedEvent<public>():listenable(healing_result)
```

Signaled when healing is applied to the healable object.

## Damage Args Structure

```verse
# Parameters for common damage functions on Fortnite objects.
damage_args<native><public> := struct:
```

Parameters for common damage functions on Fortnite objects.

### Properties

#### Instigator
```verse
# Player, agent, etc. that instigated the damage to the object.
Instigator<native><public>:?game_action_instigator = external {}
```

Player, agent, etc. that instigated the damage to the object.

#### Source
```verse
# Player, weapon, vehicle, etc. that damaged the object.
Source<native><public>:?game_action_causer = external {}
```

Player, weapon, vehicle, etc. that damaged the object.

#### Amount
```verse
# Amount of damage to apply to the object.
Amount<native><public>:float
```

Amount of damage to apply to the object.

## Damage Result Structure

```verse
# Results for damage events on Fortnite objects.
damage_result<native><public> := struct<epic_internal>:
```

Results for damage events on Fortnite objects.

### Properties

#### Target
```verse
# Object that was damaged.
Target<native><public>:damageable
```

Object that was damaged.

#### Amount
```verse
# Amount of damage applied to `Target`.
Amount<native><public>:float
```

Amount of damage applied to Target.

#### Instigator
```verse
# Player, agent, etc. that instigated the damage to `Target`. Can be false when damage is instigated by code, the environment, etc.
Instigator<native><public>:?game_action_instigator = external {}
```

Player, agent, etc. that instigated the damage to Target. Can be false when damage is instigated by code, the environment, etc.

#### Source
```verse
# Player, weapon, vehicle, etc. that damaged `Target`. Can be false when damage is caused by code, the environment, etc.
Source<native><public>:?game_action_causer = external {}
```

Player, weapon, vehicle, etc. that damaged Target. Can be false when damage is caused by code, the environment, etc.

## Healing Args Structure

```verse
# Parameters for common healing functions on Fortnite objects.
healing_args<native><public> := struct:
```

Parameters for common healing functions on Fortnite objects.

### Properties

#### Instigator
```verse
# Player, agents, etc. that instigated the healing of the object.
Instigator<native><public>:?game_action_instigator = external {}
```

Player, agents, etc. that instigated the healing of the object.

#### Source
```verse
# Player, weapon, vehicle, etc. that healed the object.
Source<native><public>:?game_action_causer = external {}
```

Player, weapon, vehicle, etc. that healed the object.

#### Amount
```verse
# Amount of healing to apply to the object.
Amount<native><public>:float
```

Amount of healing to apply to the object.

## Healing Result Structure

```verse
# Results for healing events on Fortnite objects.
healing_result<native><public> := struct<epic_internal>:
```

Results for healing events on Fortnite objects.

### Properties

#### Target
```verse
# Object that was healed.
Target<native><public>:healable
```

Object that was healed.

#### Amount
```verse
# Amount of healing applied to `Target`.
Amount<native><public>:float
```

Amount of healing applied to Target.

#### Instigator
```verse
# Player, agent, etc. that instigated healing of the `Target`. Can be false when damage is instigated by code, the environment, etc.
Instigator<native><public>:?game_action_instigator = external {}
```

Player, agent, etc. that instigated healing of the Target. Can be false when healing is instigated by code, the environment, etc.

#### Source
```verse
# Player, weapon, vehicle, etc. that healed `Target`. Can be false when damage is caused by code, the environment, etc.
Source<native><public>:?game_action_causer = external {}
```

Player, weapon, vehicle, etc. that healed Target. Can be false when healing is caused by code, the environment, etc.

## Game Action Interfaces

### Game Action Instigator Interface

```verse
# Implemented by Fortnite objects that initiate game actions, such as damage and heal. For example, player or agents.
# Event listeners often use `game_action_instigators` to calculate player damage scores.
game_action_instigator<native><public> := interface<epic_internal>:
```

Implemented by Fortnite objects that initiate game actions, such as damage and heal. For example, player or agents. Event listeners often use game_action_instigators to calculate player damage scores.

### Game Action Causer Interface

```verse
# Implemented by Fortnite objects that can be passed through game action events, such as damage and heal.
# For example: player, vehicle, or weapon.
# 
# Event Listeners often use `game_action_causer` to pass along additional information about what weapon caused the damage.
# Systems will then use that information for completing quests or processing game specific event logic.
game_action_causer<native><public> := interface:
```

Implemented by Fortnite objects that can be passed through game action events, such as damage and heal. For example: player, vehicle, or weapon.

Event Listeners often use game_action_causer to pass along additional information about what weapon caused the damage. Systems will then use that information for completing quests or processing game specific event logic.

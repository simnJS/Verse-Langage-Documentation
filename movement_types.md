
```verse
movement_types := module:
Walking<public>:movement_type = external {}

        Running<public>:movement_type = external {}

    navigatable<native><public> := interface<epic_internal>:

```
        # Return the current destination of the character

```verse
        GetCurrentDestination<public>()<transacts><decides>:(/UnrealEngine.com/Temporary/SpatialMath:)vector3


```
        # Navigate toward the specified target

```verse
        NavigateTo<public>(Target:navigation_target, ?MovementType:movement_type = external {}, ?ReachRadius:float = external {}, ?AllowPartialPath:logic = external {})<suspends>:navigation_result


```
        # Stop navigation

```verse
        StopNavigation<public>():void


```
        # Wait for a specific duration

```verse
        Wait<public>(?Duration:float = external {})<suspends>:void


```
        # Apply a multiplier on the movement speed (Multiplier is clamped between 0.5 and 2)

```verse
        SetMovementSpeedMultiplier<public>(Multiplier:float):void


```
    # Get the navigatable interface for the specified character

```verse
    (InCharacter:fort_character).GetNavigatable<native><public>()<transacts><decides>:navigatable


```
    # Inherit from this to create a custom NPC behavior.
    # The npc_behavior can be defined for a character in a CharacterDefinition asset, or in a npc_spawner_device.

```verse
    npc_behavior<native><public> := class<abstract>:

```
        # This function is called when the NPC is added to the simulation.

```verse
        OnBegin<native_callable><public>()<suspends>:void = external {}


```
        # This function is called when the NPC is removed from the simulation.

```verse
        OnEnd<native_callable><public>():void = external {}


```
        # Returns the agent associated with this behavior.

```verse
        GetAgent<native><public>()<transacts><decides>:agent


```
    # Returns the `npc_behavior` for `InAgent`.

```verse
    (InAgent:agent).GetNPCBehavior<native><public>()<transacts><decides>:npc_behavior

    @experimental

```
    # Returns the `entity` for `InNPCBehavior`.

```verse
    (InNPCBehavior:npc_behavior).GetEntity<native><public>()<reads><decides>:entity

    @experimental

```
    # The different alert levels of a guard.

```verse
    fort_guard_alert_level<native><public> := enum:

```
        # The guard has not detected any hostile target.

```verse
        Unaware

```
        # The guard has seen a hostile target but hasn't identified it yet.

```verse
        Suspicious

```
        # The guard has identified a hostile target but can't see it any more.

```verse
        LostTarget

```
        # The guard has identified a hostile target.

```verse
        Alerted

    @experimental

```
    # Information about a perceived target.

```verse
    fort_target_info<native><public> := class<epic_internal>:
        @experimental

```
        # The source of the detection stimuli.

```verse
        Target<native><public>:entity

        @experimental

```
        # True if the target can be seen.

```verse
        HasLineOfSight<native><public>:logic

        @experimental

```
        # Attitude toward this target.

```verse
        Attitude<native><public>:team_attitude

    @experimental

```
    # Create a `navigation_target` from a `fort_target_info`.

```verse
    MakeNavigationTarget<native><public>(TargetInfo:fort_target_info):navigation_target


```


```verse
AI := module:
@experimental

```
    # Result of an AI action

```verse
    ai_action_result<native><public> := enum<open>:

```
        # The action has been successfully executed

```verse
        Success

```
        # The action has failed during its execution

```verse
        Failure

```
        # The action has been canceled before completion

```verse
        Canceled

```
        # The action was not allowed to start

```verse
        Disallowed

    focus_interface<native><public> := interface<epic_internal>:

```
        # Look At specified location. Will never complete unless interrupted.

```verse
        MaintainFocus<public>(Location:(/UnrealEngine.com/Temporary/SpatialMath:)vector3)<suspends>:void


```
        # Look At specified Agent. Will never complete unless interrupted.

```verse
        MaintainFocus<public>(Agent:agent)<suspends>:void


```
    # Get the focus_interface interface for the specified character.

```verse
    (InCharacter:fort_character).GetFocusInterface<native><public>()<transacts><decides>:focus_interface

    @experimental

```
    # Fortnite Guards AI actions management

```verse
    fort_guard_actions<native><public> := interface<epic_internal>(fort_npc_actions, fort_leashable):

```
        # Roam around the current position. Use the fort_leashable_component to specify the radius, else will roam anywhere.

```verse
        RoamAround<public>(?MovementType:movement_type = external {})<suspends>:navigation_result


```
        # Move in range to attack the current target

```verse
        MoveInRangeToAttack<public>()<suspends>:ai_action_result


```
        # Play a random emote from the character emotes bank

```verse
        PlayRandomEmote<public>()<suspends>:ai_action_result


```
        # Revive the specified target

```verse
        Revive<public>(Target:agent)<suspends>:ai_action_result


```
        # Attack the target

```verse
        Attack<public>(Target:fort_target_info)<suspends>:ai_action_result

    @experimental

```
    # Get the current fort_guard_actions interface for the specified character.

```verse
    (InCharacter:fort_character).GetFortGuardActions<native><public>()<transacts><decides>:fort_guard_actions

    @experimental

```
    # Fortnite NPC perception management

```verse
    fort_guard_perception<native><public> := interface<epic_internal>(fort_npc_perception):
        @experimental

```
        # Get information about the current target.

```verse
        GetCurrentTargetInfo<public>()<reads><decides>:fort_target_info

        @experimental

```
        # Get the current alert level of the guard.

```verse
        GetAlertLevel<public>()<reads>:fort_guard_alert_level

        @experimental

```
        # Get the current alert level of a target for the guard.

```verse
        GetAlertLevel<public>(Target:entity)<reads><decides>:fort_guard_alert_level

        @experimental

```
        # Event when the alert level of the guard has changed.

```verse
        AlertLevelChangedEvent<public>:listenable(fort_guard_alert_level)

        @experimental

```
        # Event when the current target has changed.

```verse
        CurrentTargetChangedEvent<public>:listenable(fort_target_info)

    @experimental

```
    # Get the current fort_guard_perception interface for the specified character.

```verse
    (InCharacter:fort_character).GetFortGuardPerception<native><public>()<transacts><decides>:fort_guard_perception

    fort_leashable<native><public> := interface<epic_internal>:

```
        # Set custom leash position.
        #  'InnerRadius' ranges from 0.0 to 20000.0 (in centimeters).
        #  'OuterRadius' ranges from 0.0 to 20000.0 (in centimeters) and no less than 'InnerRadius'.

```verse
        SetLeashPosition<public>(Location:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, InnerRadius:float, OuterRadius:float):void


```
        # Set the agent to be the new center of the leash.
        #  'InnerRadius' ranges from 0.0 to 20000.0 (in centimeters).
        #  'OuterRadius' ranges from 0.0 to 20000.0 (in centimeters) and no less than 'InnerRadius'.

```verse
        SetLeashAgent<public>(Agent:agent, InnerRadius:float, OuterRadius:float):void


```
        # Removes the current leash.

```verse
        ClearLeash<public>():void


```
    # Get the current fort_leashable interface for the specified character.

```verse
    (InCharacter:fort_character).GetFortLeashable<native><public>()<transacts><decides>:fort_leashable

    @experimental

```
    # Fortnite NPC AI actions management

```verse
    fort_npc_actions<native><public> := interface<epic_internal>(navigatable, focus_interface):

    @experimental

```
    # Get the current fort_npc_actions interface for the specified character.

```verse
    (InCharacter:fort_character).GetFortNPCActions<native><public>()<transacts><decides>:fort_npc_actions

    @experimental

```
    # Fortnite NPC perception management

```verse
    fort_npc_perception<native><public> := interface<epic_internal>:
        @experimental

```
        # Get the last known position of a target.

```verse
        GetLastKnownPosition<public>(Target:entity)<reads><decides>:(/UnrealEngine.com/Temporary/SpatialMath:)vector3

        @experimental

```
        # Event when a target is added.

```verse
        TargetAddedEvent<public>:listenable(fort_target_info)

        @experimental

```
        # Event when the info about a target has been updated.

```verse
        TargetInfoUpdatedEvent<public>:listenable(fort_target_info)

        @experimental

```
        # Event when a target was removed.

```verse
        TargetRemovedEvent<public>:listenable(entity)

        @experimental

```
        # Event when a target is seen. Sight sense must be active.

```verse
        TargetSeenEvent<public>:listenable(fort_target_info)

        @experimental

```
        # Event when a target is heard. Hearing sense must be active.

```verse
        TargetHeardEvent<public>:listenable(fort_target_info)

        @experimental

```
        # Event when a target is touched. Touch sense must be active.

```verse
        TargetTouchedEvent<public>:listenable(fort_target_info)

        @experimental

```
        # Information about all detected targets.

```verse
        var<epic_internal> DetectedTargets<public>:[]fort_target_info

    @experimental

```
    # Get the current fort_npc_perception interface for the specified character.

```verse
    (InCharacter:fort_character).GetFortNPCPerception<native><public>()<transacts><decides>:fort_npc_perception

    navigation_target<native><public> := class<epic_internal>:


```
    # Generate a navigation_target from any position

```verse
    MakeNavigationTarget<public>(Position:(/UnrealEngine.com/Temporary/SpatialMath:)vector3):navigation_target = external {}


```
    # Generate a navigation_target from an agent

```verse
    MakeNavigationTarget<native><public>(Target:agent):navigation_target

    @experimental

```
    # Generate a navigation_target from an entity

```verse
    MakeNavigationTarget<native><public>(Entity:entity):navigation_target


```
    # Result of a navigation request

```verse
    navigation_result<native><public> := enum:

```
        # The destination has been reached

```verse
        Reached

```
        # The destination has been partially reached (AllowPartialPath was used)

```verse
        PartiallyReached

```
        # Navigation has been interrupted before completion

```verse
        Interrupted

```
        # The navigating agent is blocked

```verse
        Blocked

```
        # The destination cannot be reached

```verse
        Unreachable

    movement_type<native><public> := class<concrete><final><computes><epic_internal>:


```

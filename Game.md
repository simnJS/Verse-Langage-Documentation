
```verse
Game := module:

```
# Result data for `fort_character` elimination events.

```verse
    elimination_result<native><public> := struct<epic_internal>:

```
        # The `fort_character` eliminated from the match by `EliminatingCharacter`.

```verse
        EliminatedCharacter<native><public>:fort_character


```
        # `fort_character` that eliminated `EliminatedCharacter` from the match. `EliminatingCharacter` will be false when `EliminatedCharacter` was eliminated through non-character actions, such as environmental damage.

```verse
        EliminatingCharacter<native><public>:?fort_character


```
    # This interface is implemented by the round manager living on the simulation entity.

```verse
    fort_round_manager<native><public> := interface<epic_internal>:

```
        # Subscribed callbacks will be invoked in two scenarios:
        #  - When a new Fortnite round starts
        #  - If a round is ongoing, your callback will be invoked immediately
        # Upon the round ending, all callbacks will be canceled

```verse
        SubscribeRoundStarted<public>(Callback:type {_()<suspends>:void}):cancelable


```
        # Subscribed callbacks will be invoked when a Fortnite round ends

```verse
        SubscribeRoundEnded<public>(Callback:type {_():void}):cancelable


```
    # Returns the round manager from the simulation entity.

```verse
    (InEntity:entity).GetFortRoundManager<public>()<transacts><decides>:fort_round_manager = external {}


```
    # Implemented by objects to allow reading position information.

```verse
    positional<native><public> := interface<epic_internal>:

```
        # Returns the transform of the object.

```verse
        GetTransform<public>()<transacts>:(/UnrealEngine.com/Temporary/SpatialMath:)transform


```
    # Implemented by Fortnite objects that have health state and can be eliminated.

```verse
    healthful<native><public> := interface<epic_internal>:

```
        # Returns the health state of the object. This value will be between 0.0 and `GetMaxHealth`

```verse
        GetHealth<public>()<transacts>:float


```
        # Sets the health state of the object to `Health`.
        #  * Health state will be clamped between 1.0 and `GetMaxHealth`.
        #  * Health state cannot be directly set to 0.0. To eliminate `healthful` objects use the `damageable.Damage` functions instead.

```verse
        SetHealth<public>(Health:float)<transacts>:void


```
        # Returns the maximum health of the object. This value will be between 1.0 and Inf.

```verse
        GetMaxHealth<public>()<transacts>:float


```
        # Sets the maximum health state of the object.
        #  * MaxHealth will be clamped between 1.0 and Inf.
        #  * Current health state will be scaled up or down based on the scale difference between the old and new MaxHealth state.

```verse
        SetMaxHealth<public>(MaxHealth:float)<transacts>:void


```
    # Implemented by Fortnite objects that have shields. A shield is a method of protection that can take incoming damage while leaving the health state unchanged.

```verse
    shieldable<native><public> := interface<epic_internal>:

```
        # Returns the shield state of the object. This value will be between 0.0 and `MaxShield`

```verse
        GetShield<public>()<transacts>:float


```
        # Sets the shield state of the object.
        #  * Shield state will be clamped between 0.0 and `MaxShield`.

```verse
        SetShield<public>(Shield:float)<transacts>:void


```
        # Returns the maximum shield state of the object. This value will be between 0.0 and Inf.

```verse
        GetMaxShield<public>()<transacts>:float


```
        # Sets the maximum shield state of the object.
        #  * MaxShield will be clamped between 0.0 and Inf.
        #  * Current shield state will be scaled up or down based on the scale difference between the old and new MaxShield state.

```verse
        SetMaxShield<public>(MaxShield:float)<transacts>:void


```
        # Signaled when the shield is damaged.

```verse
        DamagedShieldEvent<public>():listenable(damage_result)


```
        # Signaled when the shield is healed.

```verse
        HealedShieldEvent<public>():listenable(healing_result)


```
    # Implemented by Fortnite objects that can be damaged.

```verse
    damageable<native><public> := interface<epic_internal>:

```
        # Damage the `damageable` object anonymously by `Amount`. Setting `Amount` to less than 0 will cause no damage.
        # Use `Damage(:damage_args):void` when damage is being applied from a known instigator and source.

```verse
        Damage<public>(Amount:float):void


```
        # Damage the `damageable` object by `Args.Amount`. Setting `Amount` to less than 0 will cause no damage.

```verse
        Damage<public>(Args:damage_args):void


```
        # Signaled when damage is applied to the `damageable` object.

```verse
        DamagedEvent<public>():listenable(damage_result)


```
    # Implemented by Fortnite objects that can be healed.

```verse
    healable<native><public> := interface<epic_internal>:

```
        # Heal the `healable` object anonymously by `Amount`. Setting `Amount` to less than 0 will cause no healing.
        # Use `Heal(:healing_args):void` when healing is being applied from a known instigator and source.

```verse
        Heal<public>(Amount:float):void


```
        # Cause `Args.Amount` damage to the `damageable` object. Setting `Amount` to less than 0 will cause no damage.

```verse
        Heal<public>(Args:healing_args):void


```
        # Signaled when healing is applied to the `healable` object.

```verse
        HealedEvent<public>():listenable(healing_result)


```
    # Parameters for common damage functions on Fortnite objects.

```verse
    damage_args<native><public> := struct:

```
        # Player, agent, etc. that instigated the damage to the object.

```verse
        Instigator<native><public>:?game_action_instigator = external {}


```
        # Player, weapon, vehicle, etc. that damaged the object.

```verse
        Source<native><public>:?game_action_causer = external {}


```
        # Amount of damage to apply to the object.

```verse
        Amount<native><public>:float


```
    # Results for damage events on Fortnite objects.

```verse
    damage_result<native><public> := struct<epic_internal>:

```
        # Object that was damaged.

```verse
        Target<native><public>:damageable


```
        # Amount of damage applied to `Target`.

```verse
        Amount<native><public>:float


```
        # Player, agent, etc. that instigated the damage to `Target`. Can be false when damage is instigated by code, the environment, etc.

```verse
        Instigator<native><public>:?game_action_instigator = external {}


```
        # Player, weapon, vehicle, etc. that damaged `Target`. Can be false when damage is caused by code, the environment, etc.

```verse
        Source<native><public>:?game_action_causer = external {}


```
    # Parameters for common healing functions on Fortnite objects.

```verse
    healing_args<native><public> := struct:

```
        # Player, agents, etc. that instigated the healing of the object.

```verse
        Instigator<native><public>:?game_action_instigator = external {}


```
        # Player, weapon, vehicle, etc. that healed the object.

```verse
        Source<native><public>:?game_action_causer = external {}


```
        # Amount of healing to apply to the object.

```verse
        Amount<native><public>:float


```
    # Results for healing events on Fortnite objects.

```verse
    healing_result<native><public> := struct<epic_internal>:

```
        # Object that was healed.

```verse
        Target<native><public>:healable


```
        # Amount of healing applied to `Target`.

```verse
        Amount<native><public>:float


```
        # Player, agent, etc. that instigated healing of the `Target`. Can be false when damage is instigated by code, the environment, etc.

```verse
        Instigator<native><public>:?game_action_instigator = external {}


```
        # Player, weapon, vehicle, etc. that healed `Target`. Can be false when damage is caused by code, the environment, etc.

```verse
        Source<native><public>:?game_action_causer = external {}


```
    # Implemented by Fortnite objects that initiate game actions, such as damage and heal. For example, player or agents.
    # Event listeners often use `game_action_instigators` to calculate player damage scores.

```verse
    game_action_instigator<native><public> := interface<epic_internal>:


```
    # Implemented by Fortnite objects that can be passed through game action events, such as damage and heal.
    # For example: player, vehicle, or weapon.
    # 
    # Event Listeners often use `game_action_causer` to pass along additional information about what weapon caused the damage.
    # Systems will then use that information for completing quests or processing game specific event logic.

```verse
    game_action_causer<native><public> := interface:


```

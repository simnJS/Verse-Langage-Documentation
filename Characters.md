
```verse
Characters := module:

```
# Main API implemented by Fortnite characters.

```verse
    fort_character<native><public> := interface<unique><epic_internal>(positional, healable, healthful, damageable, shieldable, game_action_instigator, game_action_causer):

```
        # Returns the agent associated with this `fort_character`. Use this when interacting with APIs that require an `agent` reference.

```verse
        GetAgent<public>()<transacts><decides>:agent


```
        # Signaled when this `fort_character` is eliminated from the match.

```verse
        EliminatedEvent<public>():listenable(elimination_result)


```
        # Returns the rotation where this `fort_character` is looking or aiming at.

```verse
        GetViewRotation<public>()<transacts>:(/UnrealEngine.com/Temporary/SpatialMath:)rotation


```
        # Returns the location where this `fort_character` is looking or aiming from.

```verse
        GetViewLocation<public>()<transacts>:(/UnrealEngine.com/Temporary/SpatialMath:)vector3


```
        # Signaled when this `fort_character` jumps. Returns a listenable with a payload of this `fort_character`.

```verse
        JumpedEvent<public>():listenable(fort_character)


```
        # Signaled when this `fort_character` changes crouch state.
        # Sends `tuple` payload:
        #  - 0: the `fort_character` that changed crouch states.
        #  - 1: `true` if the character is crouching. `false` if the character is not crouching.

```verse
        CrouchedEvent<public>():listenable(tuple(fort_character, logic))


```
        # Signaled when this `fort_character` changes sprint state.
        # Sends `tuple` payload:
        #  - 0: the `fort_character` that changed sprint state.
        #  - 1: `true` if the character is sprinting. `false` if the character stopped sprinting.

```verse
        SprintedEvent<public>():listenable(tuple(fort_character, logic))


```
        # Succeeds if this `fort_character` is in the world and has not been eliminated. Most fort_character actions will silently fail if this fails. Please test IsActive if you want to handle these failure cases rather than allow them to silently fail.

```verse
        IsActive<public>()<transacts><decides>:void


```
        # Succeeds if this `fort_character` is in the 'Down But Not Out' state. In this state the character is down but can still be revived by teammates for a period of time.

```verse
        IsDownButNotOut<public>()<transacts><decides>:void


```
        # Succeeds if this `fort_character` is crouching.

```verse
        IsCrouching<public>()<transacts><decides>:void


```
        # Succeeds if this `fort_character` is standing on the ground.

```verse
        IsOnGround<public>()<transacts><decides>:void


```
        # Succeeds if this `fort_character` is standing in the air.

```verse
        IsInAir<public>()<transacts><decides>:void


```
        # Succeeds if this `fort_character` is inside water volume.

```verse
        IsInWater<public>()<transacts><decides>:void


```
        # Succeeds if this `fort_character` is in falling locomotion state.

```verse
        IsFalling<public>()<transacts><decides>:void


```
        # Succeeds if this `fort_character` is in gliding locomotion state.

```verse
        IsGliding<public>()<transacts><decides>:void


```
        # Succeeds if this `fort_character` is in flying locomotion state.

```verse
        IsFlying<public>()<transacts><decides>:void


```
        # Puts this `fort_character` into stasis, preventing certain types of movement specified by `Args`.

```verse
        PutInStasis<public>(Args:stasis_args)<transacts>:void


```
        # Release this `fort_character` from stasis.

```verse
        ReleaseFromStasis<public>()<transacts>:void


```
        # Sets this `fort_character` visibility to visible.

```verse
        Show<public>():void


```
        # Sets this `fort_character` visibility to invisible.

```verse
        Hide<public>():void


```
        # Control if this `fort_character` can be damaged.

```verse
        SetVulnerability<public>(Vulnerable:logic)<transacts>:void


```
        # Succeeds if this `fort_character` can be damaged. Fails if this `fort_character` cannot be damaged.

```verse
        IsVulnerable<public>()<transacts><decides>:void


```
        # Teleports this `fort_character` to the provided `Position` and applies the yaw and pitch of `Rotation`. Will fail if the `Position` specified is e.g. outside of the playspace or specifies a place where the character cannot fit.

```verse
        TeleportTo<public>(Position:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, Rotation:(/UnrealEngine.com/Temporary/SpatialMath:)rotation)<transacts><decides>:void


```
    # Returns the `fort_character` for `InAgent`. Fails if `InAgent` is not a `fort_character`.

```verse
    (InAgent:agent).GetFortCharacter<native><public>()<transacts><decides>:fort_character


```
    # Returns a `game_action_instigator` interface for `InAgent`.

```verse
    (InAgent:agent).GetInstigator<native><public>()<transacts>:game_action_instigator


```
    # Returns the `agent` for `InInstigator`. Fails if `InInstigator` is not an `agent`.

```verse
    (InInstigator:game_action_instigator).GetInstigatorAgent<native><public>()<transacts><decides>:agent


```
    # Parameters for `fort_character.PutInStasis` function.

```verse
    stasis_args<native><public> := struct:

```
        # Controls if `fort_character` can still turn while in stasis.

```verse
        AllowTurning<native><public>:logic = external {}


```
        # Controls if `fort_character` can still fall while in stasis.

```verse
        AllowFalling<native><public>:logic = external {}


```
        # Controls if `fort_character` can still perform emotes while in stasis.

```verse
        AllowEmotes<native><public>:logic = external {}


```

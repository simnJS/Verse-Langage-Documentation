
```verse
Vehicles := module:

```
# Returns the `fort_vehicle` for `InCharacter`.
    # Fails if `InCharacter` is not associated with a `fort_vehicle`.

```verse
    (InCharacter:fort_character).GetVehicle<native><public>()<transacts><decides>:fort_vehicle


```
    # Main API implemented by Fortnite vehicles.

```verse
    fort_vehicle<native><public> := interface<unique><epic_internal>(positional, healthful, damageable, game_action_causer):

```
        # Succeeds if this `fort_vehicle` is standing on ground.

```verse
        IsOnGround<public>()<transacts><decides>:void


```
        # Succeeds if this `fort_vehicle` is standing in air.

```verse
        IsInAir<public>()<transacts><decides>:void


```
        # Succeeds if this `fort_vehicle` is standing in water.

```verse
        IsInWater<public>()<transacts><decides>:void


```
        # Returns an array with all the passengers of the vehicle.

```verse
        GetPassengers<public>()<transacts>:[]fort_character


```
        # Returns the fuel state of the vehicle. If the vehicle uses fuel, this value will be between 0.0 and `GetFuelCapacity`. Otherwise, this value will be -1.0.

```verse
        GetFuelRemaining<public>()<transacts>:float


```
        # Returns the maximum fuel capacity of the vehicle. If the vehicle uses fuel, this value will be between 1.0 and Inf. Otherwise, this value will be -1.0.

```verse
        GetFuelCapacity<public>()<transacts>:float


```
        # Teleports the `fort_vehicle` to the specified `Position` and `Rotation`.

```verse
        TeleportTo<public>(Position:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, Rotation:(/UnrealEngine.com/Temporary/SpatialMath:)rotation)<transacts><decides>:void


```

# Vehicles Module

This module provides functionality to interact with vehicles in Fortnite.

## GetVehicle Function

```verse
Vehicles := module:
    # Returns the `fort_vehicle` for `InCharacter`.
    # Fails if `InCharacter` is not associated with a `fort_vehicle`.
    (InCharacter:fort_character).GetVehicle<native><public>()<transacts><decides>:fort_vehicle
```

Retrieves the vehicle associated with a character. Fails if the character is not associated with a vehicle.

## Fort Vehicle Interface

```verse
# Main API implemented by Fortnite vehicles.
fort_vehicle<native><public> := interface<unique><epic_internal>(positional, healthful, damageable, game_action_causer):
```

Main interface implemented by Fortnite vehicles.

### Environment Detection Methods

#### IsOnGround
```verse
# Succeeds if this `fort_vehicle` is standing on ground.
IsOnGround<public>()<transacts><decides>:void
```

Succeeds if the vehicle is on the ground.

#### IsInAir
```verse
# Succeeds if this `fort_vehicle` is standing in air.
IsInAir<public>()<transacts><decides>:void
```

Succeeds if the vehicle is in the air.

#### IsInWater
```verse
# Succeeds if this `fort_vehicle` is standing in water.
IsInWater<public>()<transacts><decides>:void
```

Succeeds if the vehicle is in water.

### Passenger Management

#### GetPassengers
```verse
# Returns an array with all the passengers of the vehicle.
GetPassengers<public>()<transacts>:[]fort_character
```

Returns an array containing all passengers of the vehicle.

### Fuel Management

#### GetFuelRemaining
```verse
# Returns the fuel state of the vehicle. If the vehicle uses fuel, this value will be between 0.0 and `GetFuelCapacity`. Otherwise, this value will be -1.0.
GetFuelRemaining<public>()<transacts>:float
```

Returns the fuel state of the vehicle:
- If the vehicle uses fuel: value between 0.0 and `GetFuelCapacity`
- Otherwise: -1.0

#### GetFuelCapacity
```verse
# Returns the maximum fuel capacity of the vehicle. If the vehicle uses fuel, this value will be between 1.0 and Inf. Otherwise, this value will be -1.0.
GetFuelCapacity<public>()<transacts>:float
```

Returns the maximum fuel capacity of the vehicle:
- If the vehicle uses fuel: value between 1.0 and Inf
- Otherwise: -1.0

### Movement

#### TeleportTo
```verse
# Teleports the `fort_vehicle` to the specified `Position` and `Rotation`.
TeleportTo<public>(Position:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, Rotation:(/UnrealEngine.com/Temporary/SpatialMath:)rotation)<transacts><decides>:void
```

Teleports the vehicle to the specified position and rotation.


```verse
SpatialMath := module:
@import_as("/*.FVRotation")
    rotation<native><public> := struct<concrete>:

    @available {MinUploadedAtFNVersion := 3600}

```
    # Makes a `rotation` from `Axis` and `Angle` in radians using a right-handed sign convention (e.g. a positive rotation around Up takes Forward to Left).

```verse
    MakeRotationRadians<native><public>(Axis:vector3, Angle:float)<reads><converges>:rotation

    @available {MinUploadedAtFNVersion := 3600}

```
    # Degrees version of `MakeRotationRadians`

```verse
    MakeRotationDegrees<public>(Axis:vector3, Angle:float)<reads>:rotation = external {}

    @available {MinUploadedAtFNVersion := 3600}

```
    # Makes a `rotation` by applying a pre-rotation of `YawAngle` followed by `PitchAngle` and then `RollAngle`, in that order:
    #  * *yaw* is right-handed rotation about the Down axis,
    #  * *pitch* is right-handed rotation about the Right axis,
    #  * *roll* is right-handed rotation about the Forward axis.

```verse
    MakeRotationFromYawPitchRollRadians<public>(YawAngle:float, PitchAngle:float, RollAngle:float)<reads>:rotation = external {}


```
    # Degrees version of `MakeRotationFromYawPitchRollRadians`

```verse
    MakeRotationFromYawPitchRollDegrees<native><public>(YawAngle:float, PitchAngle:float, RollAngle:float)<reads><converges>:rotation

    @available {MinUploadedAtFNVersion := 3600}

```
    # Makes a `rotation` by applying a post-rotation of `LeftAxisAngle` followed by `UpAxisAngle` and then `ForwardAxisAngle `in that order. Right-handed convention (e.g. a positive rotation around Up takes +Forward to Left).

```verse
    MakeRotationFromEulerRadians<native><public>(LeftAxisAngle:float, UpAxisAngle:float, ForwardAxisAngle:float)<reads><converges>:rotation

    @available {MinUploadedAtFNVersion := 3600}

```
    # Degrees version of `MakeRotationFromEulerRadians`

```verse
    MakeRotationFromEulerDegrees<public>(LeftAxisAngle:float, UpAxisAngle:float, ForwardAxisAngle:float)<reads>:rotation = external {}


```
    # Makes the identity `rotation`.

```verse
    IdentityRotation<native><public>()<converges>:rotation


```
    # Returns the distance between `Rotation1` and `Rotation2`. The result will be between:
    #  * `0.0`, representing equivalent rotations and
    #  * `1.0` representing rotations which are 180 degrees apart (i.e., the shortest rotation between them is 180 degrees around some axis).

```verse
    Distance<native><public>(Rotation1:rotation, Rotation2:rotation)<reads><converges>:float

    @available {MinUploadedAtFNVersion := 3600}

```
    # Returns the smallest angular distance between `Rotation1` and `Rotation2` in radians.

```verse
    AngularDistanceRadians<native><public>(Rotation1:rotation, Rotation2:rotation)<reads><converges>:float

    @available {MinUploadedAtFNVersion := 3600}

```
    # Degrees version of `AngularDistanceRadians`.

```verse
    AngularDistanceDegrees<public>(Rotation1:rotation, Rotation2:rotation)<reads>:float = external {}

    @available {MinUploadedAtFNVersion := 3600}

```
    # Apply a `PreRotation` to `PostRotation` as `v * PreRotation * PostRotation`.

```verse
    (/Verse.org/SpatialMath:)operator'*'<native><public>(PreRotation:rotation, PostRotation:rotation)<reads><converges>:rotation

    @available {MinUploadedAtFNVersion := 3600}

```
    # Makes a `tuple(float, float, float)` with three elements:
    #  * *yaw* of `rotation` in radians
    #  * *pitch* of `rotation` in radians
    #  * *roll* of `rotation` in radians
    # using the conventions of `MakeRotationFromYawPitchRollRadians`.

```verse
    (Rotation:rotation).GetYawPitchRollRadians<public>()<reads>:tuple(float, float, float) = external {}

    @available {MinUploadedAtFNVersion := 3600}

```
    # Degrees version of `GetYawPitchRollRadians`.

```verse
    (Rotation:rotation).GetYawPitchRollDegrees<native><public>()<reads><converges>:tuple(float, float, float)

    @available {MinUploadedAtFNVersion := 3600}

```
    # Makes a `tuple(float, float, float)` with three elements:
    #  * *left axis* `rotation` in radians
    #  * *up axis* of `rotation` in radians
    #  * *forward axis* of `rotation` in radians
    # using the conventions of `MakeRotationEulerRadians`.

```verse
    (Rotation:rotation).GetEulerRadians<native><public>()<reads><converges>:tuple(float, float, float)

    @available {MinUploadedAtFNVersion := 3600}

```
    # Degrees version of `GetEulerRadians`.

```verse
    (Rotation:rotation).GetEulerDegrees<public>()<reads>:tuple(float, float, float) = external {}


```
    # Makes a `vector3` from the axis of `rotation` for an right-handed angle.
    # If `rotation` is nearly identity, this will return the +Forward axis. See also `GetAngleRadians`.

```verse
    (Rotation:rotation).GetAxis<native><public>()<reads><converges>:vector3

    @available {MinUploadedAtFNVersion := 3600}

```
    # Returns the radians of right-handed `rotation` around the axis of `rotation`. See also `GetAxis`.

```verse
    (Rotation:rotation).GetAngleRadians<native><public>()<reads><converges>:float

    @available {MinUploadedAtFNVersion := 3600}

```
    # Degrees version of GetAngleRadians

```verse
    (Rotation:rotation).GetAngleDegrees<public>()<reads>:float = external {}


```
    # Makes the smallest angular `rotation` from `InitialVector` to `FinalVector` two vectors of arbitrary length such that:
    # `InitialVector * MakeShortestRotationBetween(InitialVector, FinalVector) = FinalVector` and
    # `MakeShortestRotationBetween(InitialVector, FinalVector)?.GetAngleRadians()` is as small as possible.

```verse
    MakeShortestRotationBetween<native><public>(InitialVector:vector3, FinalVector:vector3)<reads><converges>:rotation


```
    # Used to perform spherical linear interpolation between `From` (when `Ratio = 0.0`) and `To` (when `Ratio = 1.0`). Expects `0.0 <= Ratio <= 1.0`.

```verse
    Slerp<native><public>(InitialRotation:rotation, FinalRotation:rotation, Ratio:float)<reads><converges>:rotation


```
    # Makes a `vector3` by applying `Rotation` to `Vector`.

```verse
    (/Verse.org/SpatialMath:)operator'*'<native><public>(Vector:vector3, Rotation:rotation)<reads><converges>:vector3


```
    # Makes a `rotation` by inverting `Rotation` such that `ApplyRotation(Rotation, Rotation.Invert())) = IdentityRotation`.

```verse
    (Rotation:rotation).Invert<native><public>()<reads><converges>:rotation


```
    # Returns `Rotation` if it does not contain `NaN`, `Inf` or `-Inf`.

```verse
    (Rotation:rotation).(/Verse.org/SpatialMath:)IsFinite<native><public>()<decides><converges>:rotation


```
    # Makes a unit `vector3` pointing in the *forward* rotated direction.
    # This is equivalent to: `vector3{Forward:=1.0, Left:=0.0, Up:=0.0} * Rotation`.

```verse
    (Rotation:rotation).GetForwardAxis<public>()<reads>:vector3 = external {}


```
    # Makes a unit `vector3` pointing in the *left* rotated direction.
    # This is equivalent to: `vector3{Forward:=0.0, Left:=1.0, Up:=0.0} * Rotation`.

```verse
    (Rotation:rotation).GetLeftAxis<public>()<reads>:vector3 = external {}


```
    # Makes a unit `vector3` pointing in the *up* rotated direction.
    # This is equivalent to: `vector3{Forward:=0.0, Left:=0.0, Up:=1.0} * Rotation`.

```verse
    (Rotation:rotation).GetUpAxis<public>()<reads>:vector3 = external {}


```
    # Makes a `string` representation of `rotation` in axis/degrees format with a right-handed sign convention.
    # `ToString(MakeRotationRadians(vector3{Left:=0.0, Up:=0.0, Forward:=1.0}, PiFloat/2.0))` produces the string: `"{Axis = {Left=0.000000, Up=0.000000, Forward=1.000000}, Angle = 90.000000}"`.

```verse
    (/Verse.org/SpatialMath:)ToString<public>(Rotation:rotation)<reads>:string = external {}


```
    # Returns radians from `Degrees`.

```verse
    DegreesToRadians<public>(Degrees:float)<reads>:float = external {}


```
    # Returns degrees from `Radians`.

```verse
    RadiansToDegrees<public>(Radians:float)<reads>:float = external {}

    @import_as("/*.FVTransform")

```
    # A combination of scale, rotation, and translation, applied in that order.

```verse
    transform<native><public> := struct<concrete><computes>:
        @editable

```
        # The location of this `transform`.

```verse
        Translation<public>:vector3 = external {}

        @editable

```
        # The rotation of this `transform`.

```verse
        Rotation<public>:rotation = external {}

        @editable

```
        # The scale of this `transform`.

```verse
        Scale<public>:vector3 = external {}


```
    # Makes a `vector3` by applying `InTransform` to `InVector`.

```verse
    (/Verse.org/SpatialMath:)operator'*'<public>(InVector:vector3, InTransform:transform)<reads>:vector3 = external {}


```
    # Makes a `string` representation of `InTransform` where the result is on the form.
    # `"{Translation = {ToString(`InTransform.Translation`)}, Rotation = {ToString(`InTransform.Rotation`)}, Scale = {ToString(`InTransform.Scale`)}}".

```verse
    (/Verse.org/SpatialMath:)ToString<public>(InTransform:transform)<reads>:string = external {}

    @import_as("/*.FVVector3")

```
    # 3-dimensional vector with `float` components.

```verse
    vector3<native><public> := struct<concrete><computes><persistable>:
        @editable

```
        # The Left (was -Y) component of this vector.

```verse
        Left<public>:float = external {}

        @editable

```
        # The Up (was Z) component of this vector.

```verse
        Up<public>:float = external {}

        @editable

```
        # The Forward (was X) component of this vector.

```verse
        Forward<public>:float = external {}


```
    # Makes a `vector3` by inverting the `SurfaceNormal` component of `Direction`.

```verse
    ReflectVector<public>(Direction:vector3, SurfaceNormal:vector3)<reads>:vector3 = external {}


```
    # Returns the dot product of `V1` and `V2`.

```verse
    DotProduct<public>(V1:vector3, V2:vector3)<reads>:float = external {}


```
    # Returns the left-handed cross product of `V1` and `V2`.

```verse
    CrossProductLeftHanded<public>(V1:vector3, V2:vector3)<reads>:vector3 = external {}

    @available {MinUploadedAtFNVersion := 3600}

```
    # Returns the right-handed cross product of `V1` and `V2`.

```verse
    CrossProduct<public>(V1:vector3, V2:vector3)<reads>:vector3 = external {}


```
    # Returns the Euclidean distance between `V1` and `V2`.

```verse
    Distance<public>(V1:vector3, V2:vector3)<reads>:float = external {}


```
    # Returns the squared Euclidean distance between `V1` and `V2`.

```verse
    DistanceSquared<public>(V1:vector3, V2:vector3)<reads>:float = external {}


```
    # Returns the 2-D Euclidean distance between `V1` and `V2` by ignoring the difference in `Up`.

```verse
    DistanceForwardLeft<public>(V1:vector3, V2:vector3)<reads>:float = external {}


```
    # Returns the squared 2-D Euclidean distance between `V1` and `V2` by ignoring their difference in `Up`.

```verse
    DistanceSquaredForwardLeft<public>(V1:vector3, V2:vector3)<reads>:float = external {}


```
    # Makes a unit length `vector3` pointing in the same direction of `V`.

```verse
    (V:vector3).MakeUnitVector<public>()<reads>:vector3 = external {}


```
    # Makes a `string` representation of `V`.

```verse
    (/Verse.org/SpatialMath:)ToString<public>(V:vector3)<reads>:string = external {}


```
    # Returns the length of `V`.

```verse
    (V:vector3).Length<public>()<reads>:float = external {}


```
    # Returns the squared length of `V`.

```verse
    (V:vector3).LengthSquared<public>()<computes>:float = external {}


```
    # Returns the length of `V` as if `V.Up = 0.0`.

```verse
    (V:vector3).LengthForwardLeft<public>()<reads>:float = external {}


```
    # Returns the squared length of `V` as if `V.Up = 0.0`.

```verse
    (V:vector3).LengthSquaredForwardLeft<public>()<reads>:float = external {}


```
    # Used to linearly interpolate/extrapolate between `From` (when `Parameter = 0.0`) and `To` (when `Parameter = 1.0`). Expects that all arguments are finite.
    # Returns `From*(1 - Parameter) + To*Parameter`.

```verse
    (/Verse.org/SpatialMath:)Lerp<public>(From:vector3, To:vector3, Parameter:float)<reads>:vector3 = external {}


```
    # Makes a `vector3` by inverting the signs of `Operand`.

```verse
    (/Verse.org/SpatialMath:)prefix'-'<public>(Operand:vector3)<computes>:vector3 = external {}


```
    # Makes a `vector3` by component-wise addition of `Left` and `Right`.

```verse
    (/Verse.org/SpatialMath:)operator'+'<public>(Left:vector3, Right:vector3)<computes>:vector3 = external {}


```
    # Makes a `vector3` by component-wise subtraction of `Right` from `Left`.

```verse
    (/Verse.org/SpatialMath:)operator'-'<public>(Left:vector3, Right:vector3)<computes>:vector3 = external {}


```
    # Makes a `vector3` by component-wise multiplication of `Left` and `Right`.

```verse
    (/Verse.org/SpatialMath:)operator'*'<public>(Left:vector3, Right:vector3)<computes>:vector3 = external {}


```
    # Makes a `vector3` by multiplying the components of `Left` by `Right`.

```verse
    (/Verse.org/SpatialMath:)operator'*'<public>(Left:vector3, Right:float)<computes>:vector3 = external {}


```
    # Makes a `vector3` by multiplying the components of `Right` by `Left`.

```verse
    (/Verse.org/SpatialMath:)operator'*'<public>(Left:float, Right:vector3)<computes>:vector3 = external {}


```
    # Makes a `vector3` by dividing the components of `Left` by `Right`.

```verse
    (/Verse.org/SpatialMath:)operator'/'<public>(Left:vector3, Right:float)<computes>:vector3 = external {}


```
    # Makes a `vector3` by component-wise division of `Left` by `Right`.

```verse
    (/Verse.org/SpatialMath:)operator'/'<public>(Left:vector3, Right:vector3)<computes>:vector3 = external {}


```
    # Returns `V` if all components are finite.
    # Fails if any of the components are not finite.

```verse
    (V:vector3).(/Verse.org/SpatialMath:)IsFinite<public>()<computes><decides>:vector3 = external {}


```
    # Succeeds when each component of `V` is within `AbsoluteTolerance` of `0.0`.

```verse
    (V:vector3).(/Verse.org/SpatialMath:)IsAlmostZero<public>(AbsoluteTolerance:float)<computes><decides>:void = external {}


```
    # Succeeds when each component of `V1` and `V2` are within `AbsoluteTolerance` of each other.

```verse
    (/Verse.org/SpatialMath:)IsAlmostEqual<public>(V1:vector3, V2:vector3, AbsoluteTolerance:float)<computes><decides>:void = external {}

using {/Verse.org/Concurrency}


```

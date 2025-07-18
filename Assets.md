
```verse
Assets := module:
animation_sequence<native><public> := class<computes><final><epic_internal>:

    material<native><public> := class<epic_internal>:

    particle_system<native><public> := class<computes><final><epic_internal>:

    mesh<native><public> := class<computes><epic_internal>:

    sound_wave<native><public> := class<computes><final><epic_internal>:

    texture<native><public> := class<computes><final><epic_internal>:
Verse<public> := module:
    using {/Verse.org/Colors}

```
    # Writes `Message` to a dedicated `Print` log while displaying it in `Color` on the client screen for `Duration` seconds. By default, `Color` is `NamedColors.White` and `Duration` is `2.0` seconds.

```verse
    Print<native><public>(Message:string, ?Duration:float = external {}, ?Color:color = external {})<transacts>:void


```
    # Writes `Message` to a dedicated `Print` log while displaying it in `Color` on the client screen for `Duration` seconds. By default, `Color` is `NamedColors.White` and `Duration` is `2.0` seconds.

```verse
    Print<native><public>(Message:message, ?Duration:float = external {}, ?Color:color = external {})<transacts>:void


```
    # Writes `Message` to a dedicated `Print` log while displaying it in `Color` on the client screen for `Duration` seconds. By default, `Color` is `NamedColors.White` and `Duration` is `2.0` seconds.

```verse
    Print<public>(Message:diagnostic, ?Duration:float = external {}, ?Color:color = external {})<transacts>:void = external {}

```
    # Makes a flattened `array` by concatenating the elements of `Arrays`.

```verse
    Concatenate<public>(Arrays:[][]t where t:type)<computes>:[]t = external {}


```
    # Makes an `array` containing `Input`'s elements from `StartIndex` to `StopIndex-1`.
    # Fails unless `0 <= StartIndex <= StopIndex <= Input.Length`.

```verse
    (Input:[]t where t:type).Slice<public>(StartIndex:int, StopIndex:int)<computes><decides>:[]t = external {}


```
    # Makes an `array` containing `Input`'s elements from `StartIndex` to `Input.Length-1`.
    # Succeeds if `0 <= StartIndex <= Input.Length`.

```verse
    (Input:[]t where t:type).Slice<public>(StartIndex:int)<computes><decides>:[]t = external {}


```
    # Makes an `array` by inserting `ElementsToInsert` into `Input` such that the first element of `ElementsToInsert` is at `InsertionIndex`.

```verse
    (Input:[]t where t:type).Insert<public>(InsertionIndex:int, ElementsToInsert:[]t)<computes><decides>:[]t = external {}


```
    # Makes an `array` by removing the element at `IndexToRemove` from `Input`.
    # Succeeds if `0 <= IndexToRemove <= Input.Length-1`.

```verse
    (Input:[]t where t:type).RemoveElement<public>(IndexToRemove:int)<computes><decides>:[]t = external {}


```
    # Makes an `array` by removing the element at the lowest index that equals `ElementToRemove` from `Input`.
    # Fails if `Input` did not contain any instances of `ElementToRemove`.

```verse
    (Input:[]t where t:subtype(comparable)).RemoveFirstElement<public>(ElementToRemove:t)<computes><decides>:[]t = external {}


```
    # Makes an `array` by removing all elements that equal `ElementToRemove` from `Input`.

```verse
    (Input:[]t where t:subtype(comparable)).RemoveAllElements<public>(ElementToRemove:t)<computes>:[]t = external {}


```
    # Makes an `array` by replacing the element at `IndexToReplace` with `ElementToReplaceWith` in `Input`.
    # Succeeds if `0 <= IndexToReplace <= Input.Length-1`.

```verse
    (Input:[]t where t:type).ReplaceElement<public>(IndexToReplace:int, ElementToReplaceWith:t)<computes><decides>:[]t = external {}


```
    # Makes an `array` by replacing the element at the lowest index that equals `ElementToReplace` with `ElementToReplaceWith` in `Input`.
    # Fails if `Input` did not contain any instances of `ElementToReplace`.

```verse
    (Input:[]t where t:subtype(comparable)).ReplaceFirstElement<public>(ElementToReplace:t, ElementToReplaceWith:t)<computes><decides>:[]t = external {}


```
    # Makes an `array` by replacing all elements that equal `ElementToReplace` with `ElementToReplaceWith` in `Input`.

```verse
    (Input:[]t where t:subtype(comparable)).ReplaceAllElements<public>(ElementToReplace:t, ElementToReplaceWith:t)<computes>:[]t = external {}


```
    # Makes an `array` by replacing all ranges of elements that equal `ElementsToReplace` with `Replacement` in `Input`.
    # When there are multiple overlapping instances of `ElementsToReplace` in `Input`, only the position with the lowest index is replaced.

```verse
    (Input:[]t where t:subtype(comparable)).ReplaceAll<public>(ElementsToReplace:[]t, Replacement:[]t)<transacts>:[]t = external {}


```
    # Makes an `array` by removing `Input`'s elements from `StartIndex` to `StopIndex-1`.
    # Succeeds if `0 <= StartIndex <= StopIndex <= Input.Length`.

```verse
    (Input:[]t where t:type).Remove<public>(StartIndex:int, StopIndex:int)<computes><decides>:[]t = external {}


```
    # Returns the first index whose element in `Input` equals `ElementToFind`.
    # Fails if ElementToFind does not exist in the array.

```verse
    (Input:[]t where t:subtype(comparable)).Find<public>(ElementToFind:t)<computes><decides>:int = external {}


```
    # Implemented by classes that allow users to cancel an operation. For example, calling `subscribable.Subscribe` with a callback returns a `cancelable` object. Calling `Cancel` on the return object unsubscribes the callback.

```verse
    cancelable<native><public> := interface:

```
        # Prevents any current or future work from completing.

```verse
        Cancel<native_callable><public>()<transacts>:void


```
    # An opaque diagnostic message that only shows up in diagnostic logs. The format of the diagnostic may change at any time without warning and may not be inspected by Verse code.

```verse
    diagnostic<native><public> := class<computes><epic_internal>:


```
    # Concatenates two diagnostic messages.

```verse
    operator'+'<public>(Lhs:diagnostic, Rhs:diagnostic)<computes>:diagnostic = external {}


```
    # Concatenates a diagnostic message with a normal string, yielding a diagnostic message.

```verse
    operator'+'<public>(Lhs:diagnostic, Rhs:string)<computes>:diagnostic = external {}


```
    # Concatenates a normal string with a diagnostic message, yielding a diagnostic message.

```verse
    operator'+'<public>(Lhs:string, Rhs:diagnostic)<computes>:diagnostic = external {}


```
    # Converts any Verse value into an opaque diagnostic message.

```verse
    ToDiagnostic<native><public>(Value:any)<reads>:diagnostic


```
    # Implemented by classes whose instances have limited lifetimes.

```verse
    disposable<native><public> := interface:

```
        # Cleans up this object.

```verse
        Dispose<public>():void


```
    # Implemented by classes whose instances can be enabled and disabled.

```verse
    enableable<native><public> := interface<public>:

```
        # Enable this object.

```verse
        Enable<public>():void


```
        # Disable this object.

```verse
        Disable<public>():void


```
        # Succeeds if the object is enabled, fails if it’s disabled.

```verse
        IsEnabled<public>()<transacts><decides>:void


```
    # Halts the Verse runtime with error `Message`.

```verse
    Err<native><public>(Message:string)<computes>:false


```
    # A *recurring*, successively signaled parametric `event` with a `payload` allowing a simple mechanism to coordinate between concurrent tasks.

```verse
    event<native><public>(t:type) := class(signalable(t), awaitable(t)):

```
        # Suspends the current task until another task calls `Signal`.
        # If called during another invocation of `Signal`, the the task will still suspend and resume during the next call to `Signal`.

```verse
        Await<native><override>()<suspends>:t


```
        # Concurrently resumes the tasks that were suspended by `Await` calls before this call to `Signal`.
        # 
        # Tasks are resumed in the order they were suspended. Each task will perform as much work as it can until it encounters a blocking call, whereupon it will transfer control to the next suspended task.

```verse
        Signal<native><override>(Val:t):void


```
    # A *recurring*, successively signaled event allowing a simple mechanism to coordinate between concurrent tasks.

```verse
    event<public>() := event(tuple())


```
    # Returns the smallest `int` that is greater than or equal to `Val`.
    # Fails if `not IsFinite(Val)`.

```verse
    Ceil<native><public>(Val:float)<reads><decides>:int


```
    # Returns the largest `int` that is less than or equal to `Val`.
    # Fails if `not IsFinite(Val)`.

```verse
    Floor<native><public>(Val:float)<reads><decides>:int


```
    # Returns `Val` rounded to the nearest `int`. When the fractional part of `Val` is `0.5`, rounds to the nearest *even* `int` (per the IEEE-754 default rounding mode).
    # Fails if `not IsFinite(Val)`.

```verse
    Round<native><public>(Val:float)<reads><decides>:int


```
    # Returns the `int` that equals `Val` without the fractional part.
    # Fails if `not IsFinite(val)`.

```verse
    Int<native><public>(Val:float)<reads><decides>:int


```
    # Makes a `string` representation of `Val`.

```verse
    ToString<native><public>(Val:float)<reads>:string


```
    # Returns the number of seconds since January 1, 1970 UTC, ignoring leap seconds. I.e, this function implements Unix time. This function always returns the same value within the same transaction.

```verse
    GetSecondsSinceEpoch<native><public>()<reads>:float


```
    # Makes a printable `string` representation of `Val`.

```verse
    ToString<native><public>(Val:int)<computes>:string


```
    # Implemented by classes whose instances can become invalid at runtime.

```verse
    invalidatable<native><public> := interface(disposable):

```
        # Succeeds if this object is still valid.

```verse
        IsValid<public>()<transacts><decides>:void


```
    # A parametric interface combining `awaitable` and `subscribable`.

```verse
    listenable<public>(payload:type) := interface(awaitable(payload), subscribable(payload)):


```
    # A parameterless interface combining `awaitable` and `subscribable`.

```verse
    listenable<public>() := listenable(tuple())


```
    # Used for message localization.

```verse
    locale<native><public> := struct<epic_internal>:


```
    # A localizable text message.

```verse
    message<native><public> := class<epic_internal>:


```
    # Makes a `string` by localizing `Message` based on the current `locale`.

```verse
    Localize<native><public>(Message:message)<reads>:string

    localizable_value<native><epic_internal> := class:

    localizable_string<native><epic_internal> := class<internal>(localizable_value):

    MakeLocalizableValue<epic_internal>(V:string):localizable_string = external {}

    localizable_int<native><epic_internal> := class<internal>(localizable_value):

    MakeLocalizableValue<epic_internal>(V:int):localizable_int = external {}

    localizable_float<native><epic_internal> := class<internal>(localizable_value):

    MakeLocalizableValue<epic_internal>(V:float):localizable_float = external {}

    localizable_message<native><epic_internal> := class<internal>(localizable_value):

    MakeLocalizableValue<epic_internal>(V:message):localizable_message = external {}

    MakeMessageInternal<native><epic_internal>(K:string, D:string, S:[string]localizable_value)<converges>:message


```
    # Pi, the ratio of the circumference of a circle to its diameter.

```verse
    PiFloat<public>:float = external {}


```
    # Constrains the value of `Val` between `A` and `B`. Robustly handles different argument orderings.
    # Returns the median of `Val`, `A`, and `B`, such that comparisons with `NaN` operate as if `NaN > +Inf`.

```verse
    Clamp<public>(Val:float, A:float, B:float)<computes>:float = external {}

    @rtfm_always_open

```
    # Constrains the value of `Val` between `A` and `B`. Robustly handles different argument orderings.
    # Returns the median of `Val`, `A`, and `B`.

```verse
    Clamp<native><public>(Val:int, A:int, B:int)<computes>:int


```
    # Returns the minimum of `X` and `Y`.

```verse
    Min<public>(X:int, Y:int)<computes>:int = external {}


```
    # Returns the maximum of `X` and `Y`.

```verse
    Max<public>(X:int, Y:int)<computes>:int = external {}


```
    # Returns the minimum of `X` and `Y` unless either are `NaN`.
    # Returns `NaN` if either `X` or `Y` are `NaN`.

```verse
    Min<public>(X:float, Y:float)<computes>:float = external {}


```
    # Returns the maximum of `X` and `Y` unless either are `NaN`.
    # Returns `NaN` if either `X` or `Y` are `NaN`.

```verse
    Max<public>(X:float, Y:float)<computes>:float = external {}

    @rtfm_always_open

```
    # Returns the square root of `X` if `X >= 0.0`.
    # Returns `NaN` if `X < 0.0`.

```verse
    Sqrt<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the sine of `X` if `IsFinite(X)`.
    # Returns `NaN` if `not IsFinite(X)

```verse
    Sin<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the cosine of `X` if `IsFinite(X)`.
    # Returns `NaN` if `not IsFinite(X)

```verse
    Cos<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the tangent of `X` if `IsFinite(X)`.
    # Returns `NaN` if `not IsFinite(X).

```verse
    Tan<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the inverse sine (arcsine) of `X` if `-1.0 <= X <= 1.0`.

```verse
    ArcSin<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the inverse cosine (arccosine) of `X` if `-1.0 <= X <= 1.0`.

```verse
    ArcCos<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the inverse tangent (arctangent) of `X` such that:`-PiFloat/2.0 <= ArcTan(x) <= PiFloat/2.0`.

```verse
    ArcTan<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the angle in radians at the origin between a ray pointing to `(X, Y)` and the positive `X` axis such that `-PiFloat < ArcTan(Y, X) <= PiFloat`.
    # Returns 0.0 if `X=0.0 and Y=0.0`.

```verse
    ArcTan<native><public>(Y:float, X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the hyperbolic sine of `X`.

```verse
    Sinh<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the hyperbolic cosine of `X`.

```verse
    Cosh<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the hyperbolic tangent of `X`.

```verse
    Tanh<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the inverse hyperbolic sine of `X` if `IsFinite(X)`.

```verse
    ArSinh<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the inverse hyperbolic cosine of `X` if `1.0 <= X`.

```verse
    ArCosh<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the inverse hyperbolic tangent of `X` if `IsFinite(X)`.

```verse
    ArTanh<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns `A` to the power of `B`.

```verse
    Pow<native><public>(A:float, B:float)<reads>:float


```
    # Returns `X` if `X` is finite.
    # Fails if `X` is one of:`
    #  * `+Inf`
    #  * `-Inf`
    #  * `NaN`

```verse
    (X:float).IsFinite<public>()<computes><decides>:float = external {}

    @rtfm_always_open

```
    # Returns the quotient `X/Y` as defined by Euclidean division, i.e.:
    #  * `Quotient[X/Y] = Floor[X/Y]` when `Y > 0`
    #  * `Quotient[X/Y] = Ceil[X/Y]` when `Y < 0`
    #  * `Quotient[X/Y] * Y + Mod[X,Y] = X`
    # Fails if `Y = 0`.

```verse
    Quotient<native><public>(X:int, Y:int)<computes><decides>:int

    @rtfm_always_open

```
    # Returns the remainder of `X/Y` as defined by Euclidean division, i.e.:
    #  * `Mod[X,Y] = X - Quotient(X/Y)*Y`
    #  * `0 <= Mod[X,Y] < Abs(Y)`
    # Fails if `Y=0`.

```verse
    Mod<native><public>(X:int, Y:int)<computes><decides>:int

    @rtfm_always_open

```
    # Returns the natural exponent of `X`.

```verse
    Exp<native><public>(X:float)<reads>:float

    @rtfm_always_open

```
    # Returns the natural logarithm of `X`.

```verse
    Ln<native><public>(X:float)<reads>:float


```
    # Returns the base `B` logarithm of `X`.

```verse
    Log<public>(B:float, X:float)<reads>:float = external {}

    @rtfm_always_open

```
    # Used to linearly interpolate/extrapolate between `From` (when `Parameter = 0.0`) and `To` (when `Parameter = 1.0`). Expects that all arguments are finite.
    # Returns `From*(1 - Parameter) + To*Parameter`.

```verse
    Lerp<native><public>(From:float, To:float, Parameter:float)<reads>:float


```
    # Returns the sign of `Val`:
    #   * `1` if `Val > 0`
    #  * `0` if `Val = 0`
    #  * `-1` if `Val < 0`

```verse
    Sgn<public>(Val:int)<computes>:int = external {}


```
    # Returns the sign of `Val`:
    #  * `1.0` if `Val > 0.0`
    #  * `0.0` if `Val = 0.0`
    #  * `-1.0` if `Val < 0.0`
    #  * `NaN` if `Val = NaN`

```verse
    Sgn<public>(Val:float)<computes>:float = external {}


```
    # Succeeds if `Val` is within `AbsoluteTolerance` of `0.0`.

```verse
    (Val:float).IsAlmostZero<public>(AbsoluteTolerance:float)<computes><decides>:void = external {}


```
    # Succeeds if `Val1` and `Val2` are within `AbsoluteTolerance` of each other.

```verse
    IsAlmostEqual<public>(Val1:float, Val2:float, AbsoluteTolerance:float)<computes><decides>:void = external {}


```
    # A parametric interface implemented by events with a `payload` that can be signaled.
    # Can be used with `awaitable`, `subscribable`, or both (see: `listenable`).

```verse
    signalable<public>(payload:type) := interface:

```
        # Concurrently resumes the tasks waiting for this event in `awaitable.Await` and synchronously invokes any callbacks added to this event by `subscribable.Subscribe`.

```verse
        Signal<native_callable><public>(Val:payload):void


```
    # Makes a `string` by concatenating `Separator` between the elements of `Strings`.

```verse
    Join<native><public>(Strings:[]string, Separator:string)<computes>:string


```
    # Returns `String` without modification.

```verse
    ToString<public>(String:string)<computes>:string = external {}


```
    # Makes a `string` from `Character`.

```verse
    ToString<native><public>(Character:char)<computes>:string


```
    # A parametric interface implemented by events with a `payload` that can be subscribed to.
    # Matched with `signalable.`

```verse
    subscribable<public>(t:type) := interface:

```
        # Registers `Callback` to be invoked on matching calls to `signable.Signal`.
        # Returns an unsubscriber object. Call `cancelable.Cancel` on the unsubscriber to unregister `Callback`.

```verse
        Subscribe<public>(Callback:type {_(:t):void})<transacts>:cancelable


```
    # A parameterless interface implemented by events that can be subscribed to.

```verse
    subscribable<public>() := subscribable(tuple())

using {/Verse.org/Simulation}


```

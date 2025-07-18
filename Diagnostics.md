
```verse
Diagnostics := module:

```
# Enumerated presets for policies describing a desired draw duration.

```verse
        debug_draw_duration_policy<native><public> := enum:
            SingleFrame
            FiniteDuration
            Persistent


```
        # debug_draw_channel is the base class used to define debug draw channels.

```verse
        debug_draw_channel<native><public> := class<abstract>:


```
        # debug draw class to draw debug shapes on screen.

```verse
        debug_draw<native><public> := class:

```
            # Channel will be used to clear specific debug draw.

```verse
            Channel<native><public>:subtype(debug_draw_channel) = external {}


```
            # Show Debug Draw for the channel for all users.

```verse
            ShowChannel<native><public>()<transacts>:void


```
            # Hide Debug Draw for the channel for all users.

```verse
            HideChannel<native><public>()<transacts>:void


```
            # Clears all debug draw for the channel.

```verse
            ClearChannel<native><public>()<transacts>:void


```
            # Clears all debug draw from this debug_draw instance.

```verse
            Clear<native><public>()<transacts>:void


```
            # Draws a sphere at the named location, and using the provided draw parameters.

```verse
            DrawSphere<public>(Center:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, ?Radius:float = external {}, ?Color:color = external {}, ?NumSegments:int = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}


```
            # Draws a box at the named location, and using the provided draw parameters

```verse
            DrawBox<public>(Center:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, Rotation:(/UnrealEngine.com/Temporary/SpatialMath:)rotation, ?Extent:(/UnrealEngine.com/Temporary/SpatialMath:)vector3 = external {}, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}


```
            # Draws a capsule at the named location, and using the provided draw parameters.

```verse
            DrawCapsule<public>(Center:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, Rotation:(/UnrealEngine.com/Temporary/SpatialMath:)rotation, ?Height:float = external {}, ?Radius:float = external {}, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}


```
            # Draws a cone at the named location, and using the provided draw parameters.

```verse
            DrawCone<public>(Origin:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, Direction:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, ?Height:float = external {}, ?NumSides:int = external {}, ?AngleWidthRadians:float = external {}, ?AngleHeightRadians:float = external {}, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}


```
            # Draws a cylinder at the named location, and using the provided draw parameters.

```verse
            DrawCylinder<public>(Start:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, End:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, ?NumSegments:int = external {}, ?Radius:float = external {}, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}


```
            # Draws a line from Start to End locations, and using the provided draw parameters.

```verse
            DrawLine<public>(Start:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, End:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}


```
            # Draws a point at the named location, and using the provided draw parameters.

```verse
            DrawPoint<public>(Position:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}


```
            # Draws an arrow pointing from Start to End locations, and using the provided draw parameters.

```verse
            DrawArrow<public>(Start:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, End:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, ?ArrowSize:float = external {}, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}


```
        # log levels available for various log commands

```verse
        log_level<native><public> := enum:
            Debug
            Verbose
            Normal
            Warning
            Error


```
        # log_channel is the base class used to define log channels. When printing a message to a log, the log channel class name will be prefixed to the output message.

```verse
        log_channel<native><public> := class<abstract>:


```
        # log class to send messages to the default log

```verse
        log<native><public> := class:

```
            # Channel class name will be added as a prefix used when printing the message e.g. '[log_channel]: #Message

```verse
            Channel<native><public>:subtype(log_channel)


```
            # Sets the default log level of the displayed message. See log_level enum for more info on log levels. Defaults to log_level.Normal.

```verse
            DefaultLevel<native><public>:log_level = external {}


```
            # Print message using the given log level

```verse
            (/UnrealEngine.com/Temporary/Diagnostics/log:)Print<public>(Message:string, ?Level:log_level = external {})<computes>:void = external {}


```
            # Print diagnostic using the given log level

```verse
            (/UnrealEngine.com/Temporary/Diagnostics/log:)Print<public>(Message:diagnostic, ?Level:log_level = external {})<computes>:void = external {}


```
            # Prints the current script call stack using the given log level

```verse
            PrintCallStack<native><public>(?Level:log_level = external {})<computes>:void

    using {/Verse.org/SpatialMath}
    using {/Verse.org/Native}


```

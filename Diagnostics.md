# Diagnostics Module

This module provides comprehensive debugging and diagnostic functionality for Fortnite experiences, including debug drawing and logging capabilities.

## Debug Draw Duration Policy Enum

```verse
Diagnostics := module:
    # Enumerated presets for policies describing a desired draw duration.
    debug_draw_duration_policy<native><public> := enum:
        SingleFrame
        FiniteDuration
        Persistent
```

Enumerated presets for policies describing a desired draw duration:
- **SingleFrame**: Draw for a single frame
- **FiniteDuration**: Draw for a specific duration
- **Persistent**: Draw until manually cleared

## Debug Draw Channel Base Class

```verse
# debug_draw_channel is the base class used to define debug draw channels.
debug_draw_channel<native><public> := class<abstract>:
```

Base class used to define debug draw channels.

## Debug Draw Class

```verse
# debug draw class to draw debug shapes on screen.
debug_draw<native><public> := class:
```

Debug draw class to draw debug shapes on screen.

### Properties

#### Channel
```verse
# Channel will be used to clear specific debug draw.
Channel<native><public>:subtype(debug_draw_channel) = external {}
```

Channel will be used to clear specific debug draw.

#### DefaultLevel
```verse
# Sets the default log level of the displayed message. See log_level enum for more info on log levels. Defaults to log_level.Normal.
DefaultLevel<native><public>:log_level = external {}
```

Sets the default log level of the displayed message. See log_level enum for more info on log levels. Defaults to log_level.Normal.

### Channel Management

#### ShowChannel
```verse
# Show Debug Draw for the channel for all users.
ShowChannel<native><public>()<transacts>:void
```

Shows debug draw for the channel for all users.

#### HideChannel
```verse
# Hide Debug Draw for the channel for all users.
HideChannel<native><public>()<transacts>:void
```

Hides debug draw for the channel for all users.

#### ClearChannel
```verse
# Clears all debug draw for the channel.
ClearChannel<native><public>()<transacts>:void
```

Clears all debug draw for the channel.

#### Clear
```verse
# Clears all debug draw from this debug_draw instance.
Clear<native><public>()<transacts>:void
```

Clears all debug draw from this debug_draw instance.

### Shape Drawing Methods

#### DrawSphere
```verse
# Draws a sphere at the named location, and using the provided draw parameters.
DrawSphere<public>(Center:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, ?Radius:float = external {}, ?Color:color = external {}, ?NumSegments:int = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}
```

Draws a sphere at the specified location with customizable parameters:
- **Center**: Position of the sphere
- **Radius**: Size of the sphere (optional)
- **Color**: Color of the sphere (optional)
- **NumSegments**: Number of segments for the sphere (optional)
- **Thickness**: Line thickness (optional)
- **DrawDurationPolicy**: How long to display (optional)
- **Duration**: Specific duration if using FiniteDuration policy (optional)

#### DrawBox
```verse
# Draws a box at the named location, and using the provided draw parameters
DrawBox<public>(Center:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, Rotation:(/UnrealEngine.com/Temporary/SpatialMath:)rotation, ?Extent:(/UnrealEngine.com/Temporary/SpatialMath:)vector3 = external {}, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}
```

Draws a box at the specified location with customizable parameters:
- **Center**: Position of the box
- **Rotation**: Orientation of the box
- **Extent**: Size/extent of the box (optional)
- **Color**: Color of the box (optional)
- **Thickness**: Line thickness (optional)
- **DrawDurationPolicy**: How long to display (optional)
- **Duration**: Specific duration if using FiniteDuration policy (optional)

#### DrawCapsule
```verse
# Draws a capsule at the named location, and using the provided draw parameters.
DrawCapsule<public>(Center:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, Rotation:(/UnrealEngine.com/Temporary/SpatialMath:)rotation, ?Height:float = external {}, ?Radius:float = external {}, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}
```

Draws a capsule at the specified location with customizable parameters:
- **Center**: Position of the capsule
- **Rotation**: Orientation of the capsule
- **Height**: Height of the capsule (optional)
- **Radius**: Radius of the capsule (optional)
- **Color**: Color of the capsule (optional)
- **Thickness**: Line thickness (optional)
- **DrawDurationPolicy**: How long to display (optional)
- **Duration**: Specific duration if using FiniteDuration policy (optional)

#### DrawCone
```verse
# Draws a cone at the named location, and using the provided draw parameters.
DrawCone<public>(Origin:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, Direction:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, ?Height:float = external {}, ?NumSides:int = external {}, ?AngleWidthRadians:float = external {}, ?AngleHeightRadians:float = external {}, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}
```

Draws a cone at the specified location with customizable parameters:
- **Origin**: Base position of the cone
- **Direction**: Direction the cone points
- **Height**: Height of the cone (optional)
- **NumSides**: Number of sides for the cone (optional)
- **AngleWidthRadians**: Width angle in radians (optional)
- **AngleHeightRadians**: Height angle in radians (optional)
- **Color**: Color of the cone (optional)
- **Thickness**: Line thickness (optional)
- **DrawDurationPolicy**: How long to display (optional)
- **Duration**: Specific duration if using FiniteDuration policy (optional)

#### DrawCylinder
```verse
# Draws a cylinder at the named location, and using the provided draw parameters.
DrawCylinder<public>(Start:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, End:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, ?NumSegments:int = external {}, ?Radius:float = external {}, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}
```

Draws a cylinder between two points with customizable parameters:
- **Start**: Start position of the cylinder
- **End**: End position of the cylinder
- **NumSegments**: Number of segments for the cylinder (optional)
- **Radius**: Radius of the cylinder (optional)
- **Color**: Color of the cylinder (optional)
- **Thickness**: Line thickness (optional)
- **DrawDurationPolicy**: How long to display (optional)
- **Duration**: Specific duration if using FiniteDuration policy (optional)

#### DrawLine
```verse
# Draws a line from Start to End locations, and using the provided draw parameters.
DrawLine<public>(Start:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, End:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}
```

Draws a line between two points with customizable parameters:
- **Start**: Start position of the line
- **End**: End position of the line
- **Color**: Color of the line (optional)
- **Thickness**: Line thickness (optional)
- **DrawDurationPolicy**: How long to display (optional)
- **Duration**: Specific duration if using FiniteDuration policy (optional)

#### DrawPoint
```verse
# Draws a point at the named location, and using the provided draw parameters.
DrawPoint<public>(Position:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}
```

Draws a point at the specified location with customizable parameters:
- **Position**: Position of the point
- **Color**: Color of the point (optional)
- **Thickness**: Point thickness (optional)
- **DrawDurationPolicy**: How long to display (optional)
- **Duration**: Specific duration if using FiniteDuration policy (optional)

#### DrawArrow
```verse
# Draws an arrow pointing from Start to End locations, and using the provided draw parameters.
DrawArrow<public>(Start:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, End:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, ?ArrowSize:float = external {}, ?Color:color = external {}, ?Thickness:float = external {}, ?DrawDurationPolicy:debug_draw_duration_policy = external {}, ?Duration:float = external {})<transacts>:void = external {}
```

Draws an arrow pointing from start to end with customizable parameters:
- **Start**: Start position of the arrow
- **End**: End position of the arrow
- **ArrowSize**: Size of the arrowhead (optional)
- **Color**: Color of the arrow (optional)
- **Thickness**: Line thickness (optional)
- **DrawDurationPolicy**: How long to display (optional)
- **Duration**: Specific duration if using FiniteDuration policy (optional)

## Log Level Enum

```verse
# log levels available for various log commands
log_level<native><public> := enum:
    Debug
    Verbose
    Normal
    Warning
    Error
```

Log levels available for various log commands:
- **Debug**: Detailed debug information
- **Verbose**: Verbose logging information
- **Normal**: Standard logging level
- **Warning**: Warning messages
- **Error**: Error messages

## Log Channel Base Class

```verse
# log_channel is the base class used to define log channels. When printing a message to a log, the log channel class name will be prefixed to the output message.
log_channel<native><public> := class<abstract>:
```

Base class used to define log channels. When printing a message to a log, the log channel class name will be prefixed to the output message.

## Log Class

```verse
# log class to send messages to the default log
log<native><public> := class:
```

Log class to send messages to the default log.

### Properties

#### Channel
```verse
# Channel class name will be added as a prefix used when printing the message e.g. '[log_channel]: #Message
Channel<native><public>:subtype(log_channel)
```

Channel class name will be added as a prefix used when printing the message (e.g., '[log_channel]: Message').

### Logging Methods

#### Print (String Message)
```verse
# Print message using the given log level
(/UnrealEngine.com/Temporary/Diagnostics/log:)Print<public>(Message:string, ?Level:log_level = external {})<computes>:void = external {}
```

Prints a string message using the given log level.

#### Print (Diagnostic Message)
```verse
# Print diagnostic using the given log level
(/UnrealEngine.com/Temporary/Diagnostics/log:)Print<public>(Message:diagnostic, ?Level:log_level = external {})<computes>:void = external {}
```

Prints a diagnostic message using the given log level.

#### PrintCallStack
```verse
# Prints the current script call stack using the given log level
PrintCallStack<native><public>(?Level:log_level = external {})<computes>:void
```

Prints the current script call stack using the given log level.

    using {/Verse.org/SpatialMath}
    using {/Verse.org/Native}


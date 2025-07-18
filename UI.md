# UI Module

This module provides comprehensive UI functionality for creating and managing user interfaces in Fortnite experiences.

## GetPlayerUI Function

```verse
UI := module:
    # Returns the `player_ui` associated with `Player`.
    # Fails if there is no `player_ui` associated with `Player`.
    GetPlayerUI<native><public>(Player:player)<transacts><decides>:player_ui
```

Retrieves the player UI associated with a player. Fails if there is no player UI associated with the player.

## Player UI Class

```verse
# The main interface for adding and removing `widget`s to a player's UI.
player_ui<native><public> := class<final><epic_internal>:
```

The main interface for adding and removing widgets to a player's UI.

### Widget Management

#### AddWidget (Default Slot)
```verse
# Adds `Widget` to this `player_ui` using default `player_ui_slot` configuration options.
AddWidget<native><public>(Widget:widget):void
```

Adds a widget to the player UI using default slot configuration options.

#### AddWidget (Custom Slot)
```verse
# Adds `Widget` to this `player_ui` using `Slot` for configuration options.
AddWidget<native><public>(Widget:widget, Slot:player_ui_slot):void
```

Adds a widget to the player UI using custom slot configuration options.

#### RemoveWidget
```verse
# Removes `Widget` from this `player_ui`.
RemoveWidget<native><public>(Widget:widget):void
```

Removes a widget from the player UI.

## Widget Base Class

```verse
# Base class for all UI elements drawn on the `player`'s screen.
widget<native><public> := class<abstract><unique><epic_internal>:
```

Base class for all UI elements drawn on the player's screen.

### Visibility Management

#### SetVisibility
```verse
# Shows or hides the `widget` without removing itself from the containing `player_ui`.
# See `widget_visibility` for details.
SetVisibility<native><public>(InVisibility:widget_visibility):void
```

Shows or hides the widget without removing it from the containing player UI.

#### GetVisibility
```verse
# Returns the current `widget_visibility` state.
GetVisibility<native><public>():widget_visibility
```

Returns the current widget visibility state.

### Interaction Management

#### SetEnabled
```verse
# Enables or disables whether the `player` can interact with this `widget`.
SetEnabled<native><public>(InIsEnabled:logic):void
```

Enables or disables player interaction with this widget.

#### IsEnabled
```verse
# `true` if this `widget` can be modified interactively by the player.
IsEnabled<native><public>():logic
```

Returns true if this widget can be modified interactively by the player.

### Hierarchy Management

#### GetParentWidget
```verse
# Returns the `widget`'s parent `widget`.
# Fails if no parent exists, such as if this `widget` is not in the `player_ui` or is itself the root `widget`.
GetParentWidget<native><public>()<transacts><decides>:widget
```

Returns the widget's parent widget. Fails if no parent exists.

#### GetRootWidget
```verse
# Returns the `widget` that added this `widget` to the `player_ui`. The root `widget` will return itself.
# Fails if this `widget` is not in the `player_ui`.
GetRootWidget<native><public>()<transacts><decides>:widget
```

Returns the root widget that added this widget to the player UI. The root widget returns itself.

## Player UI Slot Structure

```verse
# `widget` creation configuration options.
player_ui_slot<native><public> := struct:
```

Widget creation configuration options.

### Properties

#### ZOrder
```verse
# Controls `widget` rendering order. Greater values will be draw in front of lesser values.
ZOrder<native><public>:type {_X:int where 0 <= _X, _X <= 2147483647} = external {}
```

Controls widget rendering order. Greater values are drawn in front of lesser values.

#### InputMode
```verse
# Controls `widget` input event consumption.
InputMode<native><public>:ui_input_mode = external {}
```

Controls widget input event consumption.

## UI Input Mode Enum

```verse
# `widget` input consumption mode.
ui_input_mode<native><public> := enum:
```

Widget input consumption mode.

### Input Modes

#### None
```verse
# `widget` does not consume any input.
None
```

Widget does not consume any input.

#### All
```verse
# `widget` consumes all inputs
All
```

Widget consumes all inputs.

## Widget Message Structure

```verse
# Parameters for `event`s signalled by a `widget`.
widget_message<native><public> := struct:
```

Parameters for events signaled by a widget.

### Properties

#### Player
```verse
# The `player` that triggered the `event`.
Player<native><public>:player
```

The player that triggered the event.

#### Source
```verse
# The `widget` that triggered the `event`.
Source<native><public>:widget
```

The widget that triggered the event.

## Widget Visibility Enum

```verse
# Used by `widget.SetVisibility` determine how a `widget` is shown in the user interface.
widget_visibility<native><public> := enum:
```

Used by widget.SetVisibility to determine how a widget is shown in the user interface.

### Visibility States

#### Visible
```verse
# The `widget` is visible and occupies layout space.
Visible
```

The widget is visible and occupies layout space.

#### Collapsed
```verse
# The `widget` is invisible and does not occupy layout space.
Collapsed
```

The widget is invisible and does not occupy layout space.

#### Hidden
```verse
# The `widget` is invisible and occupies layout space.
Hidden
```

The widget is invisible and occupies layout space.

## Orientation Enum

```verse
# Used by`widget` orientation modes.
orientation<native><public> := enum:
```

Used by widget orientation modes.

### Orientation Types

#### Horizontal
```verse
# Orient `widget`s from left to right.
Horizontal
```

Orient widgets from left to right.

#### Vertical
```verse
# Orient `widget`s from top to bottom.
Vertical
```

Orient widgets from top to bottom.

## Horizontal Alignment Enum

```verse
# `widget` horizontal alignment mode.
horizontal_alignment<native><public> := enum:
```

Widget horizontal alignment mode.

### Alignment Options

#### Center
```verse
# Center `widget` horizontally within the slot.
Center
```

Center widget horizontally within the slot.

#### Left
```verse
# Align `widget` to the left of the slot.
Left
```

Align widget to the left of the slot.

#### Right
```verse
# Align `widget` to the right of the slot.
Right
```

Align widget to the right of the slot.

#### Fill
```verse
# `widget` fills the slot horizontally.
Fill
```

Widget fills the slot horizontally.

## Vertical Alignment Enum

```verse
# `widget` vertical alignment mode.
vertical_alignment<native><public> := enum:
```

Widget vertical alignment mode.

### Alignment Options

#### Center
```verse
# Center `widget` vertically within the slot.
Center
```

Center widget vertically within the slot.

#### Top
```verse
# Align `widget` to the top of the slot.
Top
```

Align widget to the top of the slot.

#### Bottom
```verse
# Align `widget` to the bottom of the slot.
Bottom
```

Align widget to the bottom of the slot.

#### Fill
```verse
# `widget` fills the slot vertically.
Fill
```

Widget fills the slot vertically.

## Anchors Structure

```verse
# The anchors of a `widget` determine its the position and sizing relative to its parent.
# `anchor`s range from `(0.0, 0.0)` (left, top) to `(1.0, 1.0)` (right, bottom).
anchors<native><public> := struct:
```

The anchors of a widget determine its position and sizing relative to its parent. Anchors range from (0.0, 0.0) (left, top) to (1.0, 1.0) (right, bottom).

### Properties

#### Minimum
```verse
# Holds the minimum anchors, (left, top). The valid range is between `0.0` and `1.0`.
Minimum<native><public>:vector2 = external {}
```

Holds the minimum anchors (left, top). Valid range is between 0.0 and 1.0.

#### Maximum
```verse
# Holds the maximum anchors, (right, bottom). The valid range is between `0.0` and `1.0`.
Maximum<native><public>:vector2 = external {}
```

Holds the maximum anchors (right, bottom). Valid range is between 0.0 and 1.0.

## Margin Structure

```verse
# Specifies the gap outside each edge separating a `widget` from its neighbors.
# Distance is measured in units where `1.0` unit is the width of a pixel at 1080p resolution.
margin<native><public> := struct:
```

Specifies the gap outside each edge separating a widget from its neighbors. Distance is measured in units where 1.0 unit is the width of a pixel at 1080p resolution.

### Properties

#### Left
```verse
# The left edge spacing.
Left<native><public>:float = external {}
```

The left edge spacing.

#### Top
```verse
# The top edge spacing.
Top<native><public>:float = external {}
```

The top edge spacing.

#### Right
```verse
# The right edge spacing.
Right<native><public>:float = external {}
```

The right edge spacing.

#### Bottom
```verse
# The bottom edge spacing.
Bottom<native><public>:float = external {}
```

The bottom edge spacing.

## Button Widget

```verse
# Button is a container of a single child widget slot and fires the OnClick event when the button is clicked.
button<native><public> := class<final>(widget):
```

Button is a container of a single child widget slot and fires the OnClick event when clicked.

### Properties

#### Slot
```verse
# The child widget of the button. Used only during initialization of the widget and not modified by SetSlot.
Slot<native><public>:button_slot
```

The child widget of the button. Used only during initialization.

### Methods

#### SetWidget
```verse
# Sets the child widget slot.
SetWidget<native><public>(InSlot:button_slot):void
```

Sets the child widget slot.

#### OnClick
```verse
# Subscribable event that fires when the button is clicked.
OnClick<public>():listenable(widget_message) = external {}
```

Subscribable event that fires when the button is clicked.

## Button Slot Structure

```verse
# Slot for button widget.
button_slot<native><public> := struct:
```

Slot for button widget.

### Properties

#### Widget
```verse
# The widget assigned to this slot.
Widget<native><public>:widget
```

The widget assigned to this slot.

#### HorizontalAlignment
```verse
# Horizontal alignment of the widget inside the slot.
HorizontalAlignment<native><public>:horizontal_alignment = external {}
```

Horizontal alignment of the widget inside the slot.

#### VerticalAlignment
```verse
# Vertical alignment of the widget inside the slot.
VerticalAlignment<native><public>:vertical_alignment = external {}
```

Vertical alignment of the widget inside the slot.

#### Padding
```verse
# Empty distance in pixels that surrounds the widget inside the slot. Assumes 1080p resolution.
Padding<native><public>:margin = external {}
```

Empty distance in pixels that surrounds the widget inside the slot. Assumes 1080p resolution.

## Canvas Widget

```verse
# Canvas is a container widget that allows for arbitrary positioning of widgets in the canvas' slots.
canvas<native><public> := class<final>(widget):
```

Canvas is a container widget that allows for arbitrary positioning of widgets in the canvas' slots.

### Properties

#### Slots
```verse
# The child widgets of the canvas. Used only during initialization of the widget and not modified by Add/RemoveWidget.
Slots<native><public>:[]canvas_slot = external {}
```

The child widgets of the canvas. Used only during initialization.

### Methods

#### AddWidget
```verse
# Adds a new child slot to the canvas.
AddWidget<native><public>(Slot:canvas_slot):void
```

Adds a new child slot to the canvas.

#### RemoveWidget
```verse
# Removes a slot containing the given widget.
RemoveWidget<native><public>(Widget:widget):void
```

Removes a slot containing the given widget.

## Canvas Slot Structure

```verse
# Slot for a canvas widget.
canvas_slot<native><public> := struct:
```

Slot for a canvas widget.

### Properties

#### Anchors
```verse
# The border for the margin and how the widget is resized with its parent.
# Values are defined between 0.0 and 1.0.
Anchors<native><public>:anchors = external {}
```

The border for the margin and how the widget is resized with its parent. Values are defined between 0.0 and 1.0.

#### Offsets
```verse
# The offset that defined the size and position of the widget.
# When the anchors are well defined, the Offsets.Left represent the distance in pixels from the Anchors Minimum.X, the Offsets.Bottom represent the distance in pixel from the Anchors Maximum.Y, effectively controlling the desired widget size. When the anchors are not well defined, the Offsets.Left and Offsets.Top represent the widget position and Offsets.Right and Offset.Bottom represent the widget size.
Offsets<native><public>:margin = external {}
```

The offset that defines the size and position of the widget.

#### SizeToContent
```verse
# When true we use the widget's desired size. The size calculated by the Offsets is ignored.
SizeToContent<native><public>:logic = external {}
```

When true, uses the widget's desired size. The size calculated by the Offsets is ignored.

#### Alignment
```verse
# Alignment is the pivot/origin point of the widget.
# Starting in the upper left at (0.0,0.0), ending in the lower right at (1.0,1.0).
Alignment<native><public>:vector2 = external {}
```

Alignment is the pivot/origin point of the widget. Starting in the upper left at (0.0,0.0), ending in the lower right at (1.0,1.0).

#### ZOrder
```verse
# Z Order of this slot relative to other slots in this canvas panel.
# Higher values are rendered last (and so they will appear to be on top)
ZOrder<native><public>:type {_X:int where 0 <= _X, _X <= 2147483647} = external {}
```

Z Order of this slot relative to other slots in this canvas panel. Higher values are rendered last.

#### Widget
```verse
# The widget assigned to this slot.
Widget<native><public>:widget
```

The widget assigned to this slot.

## MakeCanvasSlot Function

```verse
# Make a canvas slot for fixed position widget.
# If Size is set, then the Offsets is calculated and the SizeToContent is set to false.
# If Size is not set, then Right and Bottom are set to zero and are not used. The widget size will be automatically calculated. The SizeToContent is set to true.
# The widget is not anchored and will not move if the parent is resized.
# The Anchors is set to zero.
MakeCanvasSlot<native><public>(Widget:widget, Position:vector2, ?Size:vector2 = external {}, ?ZOrder:type {_X:int where 0 <= _X, _X <= 2147483647} = external {}, ?Alignment:vector2 = external {})<computes>:canvas_slot
```

Makes a canvas slot for fixed position widget. If Size is set, the Offsets is calculated and SizeToContent is set to false. If Size is not set, Right and Bottom are set to zero and the widget size will be automatically calculated with SizeToContent set to true. The widget is not anchored and will not move if the parent is resized.

## Color Block Widget

```verse
# A solid color widget.
color_block<native><public> := class<final>(widget):
```

A solid color widget.

### Properties

#### DefaultColor
```verse
# The color of the widget. Used only during initialization of the widget and not modified by SetColor.
DefaultColor<native><public>:color = external {}
```

The color of the widget. Used only during initialization.

#### DefaultOpacity
```verse
# The opacity of the widget. Used only during initialization of the widget and not modified by SetOpacity.
DefaultOpacity<native><public>:type {_X:float where 0.000000 <= _X, _X <= 1.000000} = external {}
```

The opacity of the widget. Used only during initialization.

#### DefaultDesiredSize
```verse
# The size this widget desired to be displayed in. Used only during initialization of the widget and not modified by SetDesiredSize.
DefaultDesiredSize<native><public>:vector2 = external {}
```

The size this widget desired to be displayed in. Used only during initialization.

### Methods

#### SetColor
```verse
# Sets the widget's color.
SetColor<native><public>(InColor:color):void
```

Sets the widget's color.

#### GetColor
```verse
# Gets the widget's color.
GetColor<native><public>():color
```

Gets the widget's color.

#### SetOpacity
```verse
# Sets the widgets's opacity.
SetOpacity<native><public>(InOpacity:type {_X:float where 0.000000 <= _X, _X <= 1.000000}):void
```

Sets the widget's opacity.

#### GetOpacity
```verse
# Gets the widget's opacity.
GetOpacity<native><public>():type {_X:float where 0.000000 <= _X, _X <= 1.000000}
```

Gets the widget's opacity.

#### SetDesiredSize
```verse
# Sets the size this widget desired to be displayed in.
SetDesiredSize<native><public>(InDesiredSize:vector2):void
```

Sets the size this widget desired to be displayed in.

#### GetDesiredSize
```verse
# Gets the size this widget desired to be displayed in.
GetDesiredSize<native><public>():vector2
```

Gets the size this widget desired to be displayed in.

## Image Tiling Enum

```verse
# Tiling options values
image_tiling<native><public> := enum:
```

Tiling options values.

### Tiling Options

#### Stretch
```verse
# Stretch the image to fit the available space.
Stretch
```

Stretch the image to fit the available space.

#### Repeat
```verse
# Repeat/Wrap the image to fill the available space.
Repeat
```

Repeat/Wrap the image to fill the available space.

## Texture Block Widget

```verse
# A widget to display a texture.
texture_block<native><public> := class(widget):
```

A widget to display a texture.

### Properties

#### DefaultImage
```verse
# The image to render. Used only during initialization of the widget and not modified by SetImage.
DefaultImage<native><public>:texture
```

The image to render. Used only during initialization.

#### DefaultTint
```verse
# Tinting applied to the image. Used only during initialization of the widget and not modified by SetTint.
DefaultTint<native><public>:color = external {}
```

Tinting applied to the image. Used only during initialization.

#### DefaultDesiredSize
```verse
# The size this widget desired to be displayed in. Used only during initialization of the widget and not modified by SetDesiredSize.
DefaultDesiredSize<native><public>:vector2 = external {}
```

The size this widget desired to be displayed in. Used only during initialization.

#### DefaultHorizontalTiling
```verse
# The horizontal tiling option. Used only during initialization of the widget and not modified by SetTiling.
DefaultHorizontalTiling<native><public>:image_tiling = external {}
```

The horizontal tiling option. Used only during initialization.

#### DefaultVerticalTiling
```verse
# The vertical tiling option. Used only during initialization of the widget and not modified by SetTiling.
DefaultVerticalTiling<native><public>:image_tiling = external {}
```

The vertical tiling option. Used only during initialization.

### Methods

#### SetImage
```verse
# Sets the image to render.
SetImage<native><public>(InImage:texture):void
```

Sets the image to render.

#### GetImage
```verse
# Gets the image to render.
GetImage<native><public>():texture
```

Gets the image to render.

#### SetTint
```verse
# Sets the tint applied to the image.
SetTint<native><public>(InColor:color):void
```

Sets the tint applied to the image.

#### GetTint
```verse
# Gets the tint applied to the image.
GetTint<native><public>():color
```

Gets the tint applied to the image.

#### SetDesiredSize
```verse
# Sets the size this widget desired to be displayed in.
SetDesiredSize<native><public>(InDesiredSize:vector2):void
```

Sets the size this widget desired to be displayed in.

#### GetDesiredSize
```verse
# Gets the size this widget desired to be displayed in.
GetDesiredSize<native><public>():vector2
```

Gets the size this widget desired to be displayed in.

#### SetTiling
```verse
# Sets the tiling option when the image is smaller than the allocated size.
SetTiling<native><public>(InHorizontalTiling:image_tiling, InVerticalTiling:image_tiling):void
```

Sets the tiling option when the image is smaller than the allocated size.

#### GetTiling
```verse
# Gets the tiling option.
GetTiling<native><public>():tuple(image_tiling, image_tiling)
```

Gets the tiling option.

## Material Block Widget

```verse
# A widget to display a material.
material_block<native><public> := class(widget):
```

A widget to display a material.

### Properties

#### DefaultImage
```verse
# The image to render. Used only during initialization of the widget and not modified by SetImage.
DefaultImage<native><public>:material
```

The image to render. Used only during initialization.

#### DefaultTint
```verse
# Tinting applied to the image. Used only during initialization of the widget and not modified by SetTint.
DefaultTint<native><public>:color = external {}
```

Tinting applied to the image. Used only during initialization.

#### DefaultDesiredSize
```verse
# The size this widget desired to be displayed in. Used only during initialization of the widget and not modified by SetDesiredSize.
DefaultDesiredSize<native><public>:vector2 = external {}
```

The size this widget desired to be displayed in. Used only during initialization.

### Methods

#### SetImage
```verse
# Sets the image to render.
SetImage<native><public>(InImage:material):void
```

Sets the image to render.

#### GetImage
```verse
# Gets the image to render.
GetImage<native><public>():material
```

Gets the image to render.

#### SetTint
```verse
# Sets the tint applied to the image.
SetTint<native><public>(InColor:color):void
```

Sets the tint applied to the image.

#### GetTint
```verse
# Gets the tint applied to the image.
GetTint<native><public>():color
```

Gets the tint applied to the image.

#### SetDesiredSize
```verse
# Sets the size this widget desired to be displayed in.
SetDesiredSize<native><public>(InDesiredSize:vector2):void
```

Sets the size this widget desired to be displayed in.

#### GetDesiredSize
```verse
# Gets the size this widget desired to be displayed in.
GetDesiredSize<native><public>():vector2
```

Gets the size this widget desired to be displayed in.

## Overlay Widget

```verse
# Overlay is a container consisting of widgets stacked on top of each other.
overlay<native><public> := class<final>(widget):
```

Overlay is a container consisting of widgets stacked on top of each other.

### Properties

#### Slots
```verse
# The child widgets of the overlay. Used only during initialization of the widget and not modified by Add/RemoveWidget.
Slots<native><public>:[]overlay_slot = external {}
```

The child widgets of the overlay. Used only during initialization.

### Methods

#### AddWidget
```verse
# Add a new child slot to the overlay. Slots are added at the end.
AddWidget<native><public>(Slot:overlay_slot):void
```

Adds a new child slot to the overlay. Slots are added at the end.

#### RemoveWidget
```verse
# Removes a slot containing the given widget
RemoveWidget<native><public>(Widget:widget):void
```

Removes a slot containing the given widget.

## Overlay Slot Structure

```verse
# Slot for an overlay widget
overlay_slot<native><public> := struct:
```

Slot for an overlay widget.

### Properties

#### Widget
```verse
# The widget assigned to this slot.
Widget<native><public>:widget
```

The widget assigned to this slot.

#### HorizontalAlignment
```verse
# Horizontal alignment of the widget inside the slot.
# This alignment is only applied after the layout space for the widget slot is created and determines the widget alignment within that space.
HorizontalAlignment<native><public>:horizontal_alignment = external {}
```

Horizontal alignment of the widget inside the slot. This alignment is only applied after the layout space for the widget slot is created.

#### VerticalAlignment
```verse
# Vertical alignment of the widget inside the slot.
# This alignment is only applied after the layout space for the widget slot is created and determines the widget alignment within that space.
VerticalAlignment<native><public>:vertical_alignment = external {}
```

Vertical alignment of the widget inside the slot. This alignment is only applied after the layout space for the widget slot is created.

#### Padding
```verse
# Empty distance in pixels that surrounds the widget inside the slot. Assumes 1080p resolution.
Padding<native><public>:margin = external {}
```

Empty distance in pixels that surrounds the widget inside the slot. Assumes 1080p resolution.

## Stack Box Widget

```verse
# Stack box is a container of a list of widgets stacked either vertically or horizontally.
stack_box<native><public> := class<final>(widget):
```

Stack box is a container of a list of widgets stacked either vertically or horizontally.

### Properties

#### Slots
```verse
# The child widgets of the stack box. Used only during initialization of the widget and not modified by Add/RemoveWidget.
Slots<native><public>:[]stack_box_slot = external {}
```

The child widgets of the stack box. Used only during initialization.

#### Orientation
```verse
# The orientation of the stack box. Either stack widgets horizontal or vertical.
Orientation<native><public>:orientation
```

The orientation of the stack box. Either stack widgets horizontal or vertical.

### Methods

#### AddWidget
```verse
# Add a new child slot to the stack box. Slots are added at the end.
AddWidget<native><public>(Slot:stack_box_slot):void
```

Adds a new child slot to the stack box. Slots are added at the end.

#### RemoveWidget
```verse
# Removes a slot containing the given widget
RemoveWidget<native><public>(Widget:widget):void
```

Removes a slot containing the given widget.

## Stack Box Slot Structure

```verse
# Slot for a stack_box widget
stack_box_slot<native><public> := struct:
```

Slot for a stack_box widget.

### Properties

#### Widget
```verse
# The widget assigned to this slot.
Widget<native><public>:widget
```

The widget assigned to this slot.

#### HorizontalAlignment
```verse
# Horizontal alignment of the widget inside the slot.
# This alignment is only applied after the layout space for the widget slot is created and determines the widget alignment within that space.
HorizontalAlignment<native><public>:horizontal_alignment = external {}
```

Horizontal alignment of the widget inside the slot. This alignment is only applied after the layout space for the widget slot is created.

#### VerticalAlignment
```verse
# Vertical alignment of the widget inside the slot.
# This alignment is only applied after the layout space for the widget slot is created and determines the widget alignment within that space.
VerticalAlignment<native><public>:vertical_alignment = external {}
```

Vertical alignment of the widget inside the slot. This alignment is only applied after the layout space for the widget slot is created.

#### Padding
```verse
# Empty distance in pixels that surrounds the widget inside the slot. Assumes 1080p resolution.
Padding<native><public>:margin = external {}
```

Empty distance in pixels that surrounds the widget inside the slot. Assumes 1080p resolution.

#### Distribution
```verse
# The available space will be distributed proportionally.
# If not set, the slot will use the desired size of the widget.
Distribution<native><public>:?float = external {}
```

The available space will be distributed proportionally. If not set, the slot will use the desired size of the widget.

## Text Justification Enum

```verse
# Text justification values:
#   Left: Justify the text logically to the left based on current culture.
#   Center: Justify the text in the center.
#   Right: Justify the text logically to the right based on current culture.
# The Left and Right value will flip when the local culture is right-to-left.
text_justification<native><public> := enum:
    Left
    Center
    Right
    InvariantLeft
    InvariantRight
```

Text justification values:
- **Left**: Justify the text logically to the left based on current culture.
- **Center**: Justify the text in the center.
- **Right**: Justify the text logically to the right based on current culture.
- **InvariantLeft**: Left justification that doesn't flip in right-to-left cultures.
- **InvariantRight**: Right justification that doesn't flip in right-to-left cultures.

The Left and Right values will flip when the local culture is right-to-left.

## Text Overflow Policy Enum

```verse
# Text overflow policy values:
#   Clip: Overflowing text will be clipped.
#   Ellipsis: Overflowing text will be replaced with an ellipsis.
text_overflow_policy<native><public> := enum:
    Clip
    Ellipsis
```

Text overflow policy values:
- **Clip**: Overflowing text will be clipped.
- **Ellipsis**: Overflowing text will be replaced with an ellipsis.

## Text Base Widget

```verse
# Base widget for text widget.
text_base<native><public> := class<abstract>(widget):
```

Base widget for text widget.

### Properties

#### DefaultText
```verse
# The text to display to the user. Used only during initialization of the widget and not modified by SetText.
DefaultText<native><localizes><public>:message = external {}
```

The text to display to the user. Used only during initialization.

#### DefaultTextColor
```verse
# The color of the displayed text. Used only during initialization of the widget and not modified by SetTextColor.
DefaultTextColor<native><public>:color = external {}
```

The color of the displayed text. Used only during initialization.

#### DefaultTextOpacity
```verse
# The opacity of the displayed text. Used only during initialization of the widget and not modified by SetTextOpacity.
DefaultTextOpacity<native><public>:type {_X:float where 0.000000 <= _X, _X <= 1.000000} = external {}
```

The opacity of the displayed text. Used only during initialization.

#### DefaultJustification
```verse
# The justification to display to the user. Used only during initialization of the widget and not modified by SetJustification.
DefaultJustification<native><public>:text_justification = external {}
```

The justification to display to the user. Used only during initialization.

#### DefaultOverflowPolicy
```verse
# The policy that determine what happens when the text is longer than its allowed length.
# Used only during initialization of the widget and not modified by SetOverflowPolicy.
DefaultOverflowPolicy<native><public>:text_overflow_policy = external {}
```

The policy that determines what happens when the text is longer than its allowed length. Used only during initialization.

### Methods

#### SetText
```verse
# Sets the text displayed in the widget.
SetText<native><public>(InText:message):void
```

Sets the text displayed in the widget.

#### GetText
```verse
# Gets the text currently in the widget.
GetText<native><public>():string
```

Gets the text currently in the widget.

#### SetJustification
```verse
# Sets the text justification in the widget.
SetJustification<native><public>(InJustification:text_justification):void
```

Sets the text justification in the widget.

#### GetJustification
```verse
# Gets the text justification in the widget.
GetJustification<native><public>():text_justification
```

Gets the text justification in the widget.

#### SetOverflowPolicy
```verse
# Sets the policy that determine what happens when the text is longer than its allowed length.
SetOverflowPolicy<native><public>(InOverflowPolicy:text_overflow_policy):void
```

Sets the policy that determines what happens when the text is longer than its allowed length.

#### GetOverflowPolicy
```verse
# Gets the policy that determine what happens when the text is longer than its allowed length.
GetOverflowPolicy<native><public>():text_overflow_policy
```

Gets the policy that determines what happens when the text is longer than its allowed length.

#### SetTextColor
```verse
# Sets the color of the displayed text.
SetTextColor<native><public>(InColor:color):void
```

Sets the color of the displayed text.

#### GetTextColor
```verse
# Gets the color of the displayed text.
GetTextColor<native><public>():color
```

Gets the color of the displayed text.

#### SetTextOpacity
```verse
# Sets the opacity of the displayed text.
SetTextOpacity<native><public>(InOpacity:type {_X:float where 0.000000 <= _X, _X <= 1.000000}):void
```

Sets the opacity of the displayed text.

#### GetTextOpacity
```verse
# Gets the opacity of the displayed text.
GetTextOpacity<native><public>():type {_X:float where 0.000000 <= _X, _X <= 1.000000}
```

Gets the opacity of the displayed text.

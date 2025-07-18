
```verse
UI := module:

```
# Returns the `player_ui` associated with `Player`.
        # Fails if there is no `player_ui` associated with `Player`.

```verse
        GetPlayerUI<native><public>(Player:player)<transacts><decides>:player_ui


```
        # The main interface for adding and removing `widget`s to a player's UI.

```verse
        player_ui<native><public> := class<final><epic_internal>:

```
            # Adds `Widget` to this `player_ui` using default `player_ui_slot` configuration options.

```verse
            AddWidget<native><public>(Widget:widget):void


```
            # Adds `Widget` to this `player_ui` using `Slot` for configuration options.

```verse
            AddWidget<native><public>(Widget:widget, Slot:player_ui_slot):void


```
            # Removes `Widget` from this `player_ui`.

```verse
            RemoveWidget<native><public>(Widget:widget):void


```
        # Base class for all UI elements drawn on the `player`'s screen.

```verse
        widget<native><public> := class<abstract><unique><epic_internal>:

```
            # Shows or hides the `widget` without removing itself from the containing `player_ui`.
            # See `widget_visibility` for details.

```verse
            SetVisibility<native><public>(InVisibility:widget_visibility):void


```
            # Returns the current `widget_visibility` state.

```verse
            GetVisibility<native><public>():widget_visibility


```
            # Enables or disables whether the `player` can interact with this `widget`.

```verse
            SetEnabled<native><public>(InIsEnabled:logic):void


```
            # `true` if this `widget` can be modified interactively by the player.

```verse
            IsEnabled<native><public>():logic


```
            # Returns the `widget`'s parent `widget`.
            # Fails if no parent exists, such as if this `widget` is not in the `player_ui` or is itself the root `widget`.

```verse
            GetParentWidget<native><public>()<transacts><decides>:widget


```
            # Returns the `widget` that added this `widget` to the `player_ui`. The root `widget` will return itself.
            # Fails if this `widget` is not in the `player_ui`.

```verse
            GetRootWidget<native><public>()<transacts><decides>:widget


```
        # `widget` creation configuration options.

```verse
        player_ui_slot<native><public> := struct:

```
            # Controls `widget` rendering order. Greater values will be draw in front of lesser values.

```verse
            ZOrder<native><public>:type {_X:int where 0 <= _X, _X <= 2147483647} = external {}


```
            # Controls `widget` input event consumption.

```verse
            InputMode<native><public>:ui_input_mode = external {}


```
        # `widget` input consumption mode.

```verse
        ui_input_mode<native><public> := enum:

```
            # `widget` does not consume any input.

```verse
            None

```
            # `widget` consumes all inputs

```verse
            All


```
        # Parameters for `event`s signalled by a `widget`.

```verse
        widget_message<native><public> := struct:

```
            # The `player` that triggered the `event`.

```verse
            Player<native><public>:player


```
            # The `widget` that triggered the `event`.

```verse
            Source<native><public>:widget


```
        # Used by `widget.SetVisibility` determine how a `widget` is shown in the user interface.

```verse
        widget_visibility<native><public> := enum:

```
            # The `widget` is visible and occupies layout space.

```verse
            Visible

```
            # The `widget` is invisible and does not occupy layout space.

```verse
            Collapsed

```
            # The `widget` is invisible and occupies layout space.

```verse
            Hidden


```
        # Used by`widget` orientation modes.

```verse
        orientation<native><public> := enum:

```
            # Orient `widget`s from left to right.

```verse
            Horizontal

```
            # Orient `widget`s from top to bottom.

```verse
            Vertical


```
        # `widget` horizontal alignment mode.

```verse
        horizontal_alignment<native><public> := enum:

```
            # Center `widget` horizontally within the slot.

```verse
            Center

```
            # Align `widget` to the left of the slot.

```verse
            Left

```
            # Align `widget` to the right of the slot.

```verse
            Right

```
            # `widget` fills the slot horizontally.

```verse
            Fill


```
        # `widget` vertical alignment mode.

```verse
        vertical_alignment<native><public> := enum:

```
            # Center `widget` vertically within the slot.

```verse
            Center

```
            # Align `widget` to the top of the slot.

```verse
            Top

```
            # Align `widget` to the bottom of the slot.

```verse
            Bottom

```
            # `widget` fills the slot vertically.

```verse
            Fill


```
        # The anchors of a `widget` determine its the position and sizing relative to its parent.
        # `anchor`s range from `(0.0, 0.0)` (left, top) to `(1.0, 1.0)` (right, bottom).

```verse
        anchors<native><public> := struct:

```
            # Holds the minimum anchors, (left, top). The valid range is between `0.0` and `1.0`.

```verse
            Minimum<native><public>:vector2 = external {}


```
            # Holds the maximum anchors, (right, bottom). The valid range is between `0.0` and `1.0`.

```verse
            Maximum<native><public>:vector2 = external {}


```
        # Specifies the gap outside each edge separating a `widget` from its neighbors.
        # Distance is measured in units where `1.0` unit is the width of a pixel at 1080p resolution.

```verse
        margin<native><public> := struct:

```
            # The left edge spacing.

```verse
            Left<native><public>:float = external {}


```
            # The top edge spacing.

```verse
            Top<native><public>:float = external {}


```
            # The right edge spacing.

```verse
            Right<native><public>:float = external {}


```
            # The bottom edge spacing.

```verse
            Bottom<native><public>:float = external {}


```
        # Button is a container of a single child widget slot and fires the OnClick event when the button is clicked.

```verse
        button<native><public> := class<final>(widget):

```
            # The child widget of the button. Used only during initialization of the widget and not modified by SetSlot.

```verse
            Slot<native><public>:button_slot


```
            # Sets the child widget slot.

```verse
            SetWidget<native><public>(InSlot:button_slot):void


```
            # Subscribable event that fires when the button is clicked.

```verse
            OnClick<public>():listenable(widget_message) = external {}


```
        # Slot for button widget.

```verse
        button_slot<native><public> := struct:

```
            # The widget assigned to this slot.

```verse
            Widget<native><public>:widget


```
            # Horizontal alignment of the widget inside the slot.

```verse
            HorizontalAlignment<native><public>:horizontal_alignment = external {}


```
            # Vertical alignment of the widget inside the slot.

```verse
            VerticalAlignment<native><public>:vertical_alignment = external {}


```
            # Empty distance in pixels that surrounds the widget inside the slot. Assumes 1080p resolution.

```verse
            Padding<native><public>:margin = external {}


```
        # Canvas is a container widget that allows for arbitrary positioning of widgets in the canvas' slots.

```verse
        canvas<native><public> := class<final>(widget):

```
            # The child widgets of the canvas. Used only during initialization of the widget and not modified by Add/RemoveWidget.

```verse
            Slots<native><public>:[]canvas_slot = external {}


```
            # Adds a new child slot to the canvas.

```verse
            AddWidget<native><public>(Slot:canvas_slot):void


```
            # Removes a slot containing the given widget.

```verse
            RemoveWidget<native><public>(Widget:widget):void


```
        # Slot for a canvas widget.

```verse
        canvas_slot<native><public> := struct:

```
            # The border for the margin and how the widget is resized with its parent.
            # Values are defined between 0.0 and 1.0.

```verse
            Anchors<native><public>:anchors = external {}


```
            # The offset that defined the size and position of the widget.
            # When the anchors are well defined, the Offsets.Left represent the distance in pixels from the Anchors Minimum.X, the Offsets.Bottom represent the distance in pixel from the Anchors Maximum.Y, effectively controlling the desired widget size. When the anchors are not well defined, the Offsets.Left and Offsets.Top represent the widget position and Offsets.Right and Offset.Bottom represent the widget size.

```verse
            Offsets<native><public>:margin = external {}


```
            # When true we use the widget's desired size. The size calculated by the Offsets is ignored.

```verse
            SizeToContent<native><public>:logic = external {}


```
            # Alignment is the pivot/origin point of the widget.
            # Starting in the upper left at (0.0,0.0), ending in the lower right at (1.0,1.0).

```verse
            Alignment<native><public>:vector2 = external {}


```
            # Z Order of this slot relative to other slots in this canvas panel.
            # Higher values are rendered last (and so they will appear to be on top)

```verse
            ZOrder<native><public>:type {_X:int where 0 <= _X, _X <= 2147483647} = external {}


```
            # The widget assigned to this slot.

```verse
            Widget<native><public>:widget


```
        # Make a canvas slot for fixed position widget.
        # If Size is set, then the Offsets is calculated and the SizeToContent is set to false.
        # If Size is not set, then Right and Bottom are set to zero and are not used. The widget size will be automatically calculated. The SizeToContent is set to true.
        # The widget is not anchored and will not move if the parent is resized.
        # The Anchors is set to zero.

```verse
        MakeCanvasSlot<native><public>(Widget:widget, Position:vector2, ?Size:vector2 = external {}, ?ZOrder:type {_X:int where 0 <= _X, _X <= 2147483647} = external {}, ?Alignment:vector2 = external {})<computes>:canvas_slot


```
        # A solid color widget.

```verse
        color_block<native><public> := class<final>(widget):

```
            # The color of the widget. Used only during initialization of the widget and not modified by SetColor.

```verse
            DefaultColor<native><public>:color = external {}


```
            # The opacity of the widget. Used only during initialization of the widget and not modified by SetOpacity.

```verse
            DefaultOpacity<native><public>:type {_X:float where 0.000000 <= _X, _X <= 1.000000} = external {}


```
            # The size this widget desired to be displayed in. Used only during initialization of the widget and not modified by SetDesiredSize.

```verse
            DefaultDesiredSize<native><public>:vector2 = external {}


```
            # Sets the widget's color.

```verse
            SetColor<native><public>(InColor:color):void


```
            # Gets the widget's color.

```verse
            GetColor<native><public>():color


```
            # Sets the widgets's opacity.

```verse
            SetOpacity<native><public>(InOpacity:type {_X:float where 0.000000 <= _X, _X <= 1.000000}):void


```
            # Gets the widget's opacity.

```verse
            GetOpacity<native><public>():type {_X:float where 0.000000 <= _X, _X <= 1.000000}


```
            # Sets the size this widget desired to be displayed in.

```verse
            SetDesiredSize<native><public>(InDesiredSize:vector2):void


```
            # Gets the size this widget desired to be displayed in.

```verse
            GetDesiredSize<native><public>():vector2


```
        # Tiling options values

```verse
        image_tiling<native><public> := enum:

```
            # Stretch the image to fit the available space.

```verse
            Stretch

```
            # Repeat/Wrap the image to fill the available space.

```verse
            Repeat


```
        # A widget to display a texture.

```verse
        texture_block<native><public> := class(widget):

```
            # The image to render. Used only during initialization of the widget and not modified by SetImage.

```verse
            DefaultImage<native><public>:texture


```
            # Tinting applied to the image. Used only during initialization of the widget and not modified by SetTint.

```verse
            DefaultTint<native><public>:color = external {}


```
            # The size this widget desired to be displayed in. Used only during initialization of the widget and not modified by SetDesiredSize.

```verse
            DefaultDesiredSize<native><public>:vector2 = external {}


```
            # The horizontal tiling option. Used only during initialization of the widget and not modified by SetTiling.

```verse
            DefaultHorizontalTiling<native><public>:image_tiling = external {}


```
            # The vertical tiling option. Used only during initialization of the widget and not modified by SetTiling.

```verse
            DefaultVerticalTiling<native><public>:image_tiling = external {}


```
            # Sets the image to render.

```verse
            SetImage<native><public>(InImage:texture):void


```
            # Gets the image to render.

```verse
            GetImage<native><public>():texture


```
            # Sets the tint applied to the image.

```verse
            SetTint<native><public>(InColor:color):void


```
            # Gets the tint applied to the image.

```verse
            GetTint<native><public>():color


```
            # Sets the size this widget desired to be displayed in.

```verse
            SetDesiredSize<native><public>(InDesiredSize:vector2):void


```
            # Gets the size this widget desired to be displayed in.

```verse
            GetDesiredSize<native><public>():vector2


```
            # Sets the tiling option when the image is smaller than the allocated size.

```verse
            SetTiling<native><public>(InHorizontalTiling:image_tiling, InVerticalTiling:image_tiling):void


```
            # Gets the tiling option.

```verse
            GetTiling<native><public>():tuple(image_tiling, image_tiling)


```
        # A widget to display a material.

```verse
        material_block<native><public> := class(widget):

```
            # The image to render. Used only during initialization of the widget and not modified by SetImage.

```verse
            DefaultImage<native><public>:material


```
            # Tinting applied to the image. Used only during initialization of the widget and not modified by SetTint.

```verse
            DefaultTint<native><public>:color = external {}


```
            # The size this widget desired to be displayed in. Used only during initialization of the widget and not modified by SetDesiredSize.

```verse
            DefaultDesiredSize<native><public>:vector2 = external {}


```
            # Sets the image to render.

```verse
            SetImage<native><public>(InImage:material):void


```
            # Gets the image to render.

```verse
            GetImage<native><public>():material


```
            # Sets the tint applied to the image.

```verse
            SetTint<native><public>(InColor:color):void


```
            # Gets the tint applied to the image.

```verse
            GetTint<native><public>():color


```
            # Sets the size this widget desired to be displayed in.

```verse
            SetDesiredSize<native><public>(InDesiredSize:vector2):void


```
            # Gets the size this widget desired to be displayed in.

```verse
            GetDesiredSize<native><public>():vector2


```
        # Overlay is a container consisting of widgets stacked on top of each other.

```verse
        overlay<native><public> := class<final>(widget):

```
            # The child widgets of the overlay. Used only during initialization of the widget and not modified by Add/RemoveWidget.

```verse
            Slots<native><public>:[]overlay_slot = external {}


```
            # Add a new child slot to the overlay. Slots are added at the end.

```verse
            AddWidget<native><public>(Slot:overlay_slot):void


```
            # Removes a slot containing the given widget

```verse
            RemoveWidget<native><public>(Widget:widget):void


```
        # Slot for an overlay widget

```verse
        overlay_slot<native><public> := struct:

```
            # The widget assigned to this slot.

```verse
            Widget<native><public>:widget


```
            # Horizontal alignment of the widget inside the slot.
            # This alignment is only applied after the layout space for the widget slot is created and determines the widget alignment within that space.

```verse
            HorizontalAlignment<native><public>:horizontal_alignment = external {}


```
            # Vertical alignment of the widget inside the slot.
            # This alignment is only applied after the layout space for the widget slot is created and determines the widget alignment within that space.

```verse
            VerticalAlignment<native><public>:vertical_alignment = external {}


```
            # Empty distance in pixels that surrounds the widget inside the slot. Assumes 1080p resolution.

```verse
            Padding<native><public>:margin = external {}


```
        # Stack box is a container of a list of widgets stacked either vertically or horizontally.

```verse
        stack_box<native><public> := class<final>(widget):

```
            # The child widgets of the stack box. Used only during initialization of the widget and not modified by Add/RemoveWidget.

```verse
            Slots<native><public>:[]stack_box_slot = external {}


```
            # The orientation of the stack box. Either stack widgets horizontal or vertical.

```verse
            Orientation<native><public>:orientation


```
            # Add a new child slot to the stack box. Slots are added at the end.

```verse
            AddWidget<native><public>(Slot:stack_box_slot):void


```
            # Removes a slot containing the given widget

```verse
            RemoveWidget<native><public>(Widget:widget):void


```
        # Slot for a stack_box widget

```verse
        stack_box_slot<native><public> := struct:

```
            # The widget assigned to this slot.

```verse
            Widget<native><public>:widget


```
            # Horizontal alignment of the widget inside the slot.
            # This alignment is only applied after the layout space for the widget slot is created and determines the widget alignment within that space.

```verse
            HorizontalAlignment<native><public>:horizontal_alignment = external {}


```
            # Vertical alignment of the widget inside the slot.
            # This alignment is only applied after the layout space for the widget slot is created and determines the widget alignment within that space.

```verse
            VerticalAlignment<native><public>:vertical_alignment = external {}


```
            # Empty distance in pixels that surrounds the widget inside the slot. Assumes 1080p resolution.

```verse
            Padding<native><public>:margin = external {}


```
            # The available space will be distributed proportionally.
            # If not set, the slot will use the desired size of the widget.

```verse
            Distribution<native><public>:?float = external {}


```
        # Text justification values:
        #   Left: Justify the text logically to the left based on current culture.
        #   Center: Justify the text in the center.
        #   Right: Justify the text logically to the right based on current culture.
        # The Left and Right value will flip when the local culture is right-to-left.

```verse
        text_justification<native><public> := enum:
            Left
            Center
            Right
            InvariantLeft
            InvariantRight


```
        # Text overflow policy values:
        #   Clip: Overflowing text will be clipped.
        #   Ellipsis: Overflowing text will be replaced with an ellipsis.

```verse
        text_overflow_policy<native><public> := enum:
            Clip
            Ellipsis


```
        # Base widget for text widget.

```verse
        text_base<native><public> := class<abstract>(widget):

```
            # The text to display to the user. Used only during initialization of the widget and not modified by SetText.

```verse
            DefaultText<native><localizes><public>:message = external {}


```
            # The color of the displayed text. Used only during initialization of the widget and not modified by SetTextColor.

```verse
            DefaultTextColor<native><public>:color = external {}


```
            # The opacity of the displayed text. Used only during initialization of the widget and not modified by SetTextOpacity.

```verse
            DefaultTextOpacity<native><public>:type {_X:float where 0.000000 <= _X, _X <= 1.000000} = external {}


```
            # The justification to display to the user. Used only during initialization of the widget and not modified by SetJustification.

```verse
            DefaultJustification<native><public>:text_justification = external {}


```
            # The policy that determine what happens when the text is longer than its allowed length.
            # Used only during initialization of the widget and not modified by SetOverflowPolicy.

```verse
            DefaultOverflowPolicy<native><public>:text_overflow_policy = external {}


```
            # Sets the text displayed in the widget.

```verse
            SetText<native><public>(InText:message):void


```
            # Gets the text currently in the widget.

```verse
            GetText<native><public>():string


```
            # Sets the text justification in the widget.

```verse
            SetJustification<native><public>(InJustification:text_justification):void


```
            # Gets the text justification in the widget.

```verse
            GetJustification<native><public>():text_justification


```
            # Sets the policy that determine what happens when the text is longer than its allowed length.

```verse
            SetOverflowPolicy<native><public>(InOverflowPolicy:text_overflow_policy):void


```
            # Gets the policy that determine what happens when the text is longer than its allowed length.

```verse
            GetOverflowPolicy<native><public>():text_overflow_policy


```
            # Sets the color of the displayed text.

```verse
            SetTextColor<native><public>(InColor:color):void


```
            # Gets the color of the displayed text.

```verse
            GetTextColor<native><public>():color


```
            # Sets the opacity of the displayed text.

```verse
            SetTextOpacity<native><public>(InOpacity:type {_X:float where 0.000000 <= _X, _X <= 1.000000}):void


```
            # Gets the opacity of the displayed text.

```verse
            GetTextOpacity<native><public>():type {_X:float where 0.000000 <= _X, _X <= 1.000000}


```


```verse
Tags := module:

```
# A single gameplay tag, which represents a hierarchical name of the form x.y that is registered in the GameplayTagsManager You can filter the gameplay tags displayed in the editor.

```verse
        tag<native><public> := class<abstract>:


```
        # A queryable collection of gameplay tags.

```verse
        tag_view<native><public> := interface<epic_internal>:

```
            # Determine if TagToCheck is present in this container, also checking against parent tags {"A.1"}.Has("A") will return True, {"A"}.Has("A.1") will return False If TagToCheck is not Valid it will always return False.

```verse
            Has<public>(TagToCheck:tag)<reads><decides>:void


```
            # Checks if this container contains ANY of the tags in the specified container, also checks against parent tags {"A.1"}.HasAny({"A","B"}) will return True, {"A"}.HasAny({"A.1","B"}) will return False If InTags is empty/invalid it will always return False.

```verse
            HasAny<public>(InTags:[]tag)<reads><decides>:void


```
            # Checks if this container contains ALL of the tags in the specified container, also checks against parent tags {"A.1","B.1"}.HasAll({"A","B"}) will return True, {"A","B"}.HasAll({"A.1","B.1"}) will return False If InTags is empty/invalid it will always return True, because there were no failed checks.

```verse
            HasAll<public>(InTags:[]tag)<reads><decides>:void

        tag_search_sort_type<native><public> := enum:
            Unsorted
            Sorted


```
        # Advanced tag search criteria

```verse
        tag_search_criteria<native><public> := class:

```
            # Tags required to be on the object.

```verse
            RequiredTags<native><public>:[]tag = external {}


```
            # Tags that are used if no required tags are specified. These are treated as if any of them will do.

```verse
            PreferredTags<native><public>:[]tag = external {}


```
            # Tags that may NOT be on the object. All items with these tags are excluded from the search.

```verse
            ExclusionTags<native><public>:[]tag = external {}


```
            # Flag to request sorting the results by tag.

```verse
            SortType<native><public>:tag_search_sort_type = external {}

    @attribscope_class
    @attribscope_struct
    @attribscope_data
    @customattribhandler
    editable<public> := class<computes>(attribute):

```
        # The tooltip displayed in the editor.

```verse
        ToolTip<public>:message = external {}


```
        # The categories displayed in the editor.

```verse
        Categories<public>:[]message = external {}

    @attribscope_class
    @attribscope_struct
    @attribscope_data
    @customattribhandler
    editable_text_box<public> := class<final><computes>(editable):

```
        # True if the editor text box should support multiple lines.

```verse
        MultiLine<public>:logic = external {}


```
        # The maximum length of the text.

```verse
        MaxLength<public>:int = external {}

    @attribscope_class
    @attribscope_struct
    @attribscope_data
    @customattribhandler
    editable_slider<public>(t:type) := class<final><computes>(editable):

```
        # The minimum value of the editor slider.

```verse
        MinValue<public>:?t = external {}


```
        # The maximum value of the editor slider.

```verse
        MaxValue<public>:?t = external {}


```
        # The amount the slider moves for each step.

```verse
        SliderDelta<public>:?t = external {}


```
        # Used to scale a slider exponentially. Common values are found within the range of 1-20.

```verse
        SliderExponent<public>:?t = external {}


```
        # Used to change how sensitive the field value is when moving the slider via mouse cursor.

```verse
        MouseLinearDeltaSensitivity<public>:float = external {}

        MouseShiftMovePixelPerDelta<public>:float = external {}

    @attribscope_class
    @attribscope_struct
    @attribscope_data
    @customattribhandler
    editable_number<public>(t:type) := class<final><computes>(editable):

```
        # The minimum value the editor allows.

```verse
        MinValue<public>:?t = external {}


```
        # The maximum value the editor allows.

```verse
        MaxValue<public>:?t = external {}


```
        # Snap the spinbox to the nearest delta.

```verse
        SpinBoxDelta<public>:?t = external {}

    @attribscope_class
    @attribscope_struct
    @attribscope_data
    @customattribhandler
    editable_vector_slider<public>(t:type) := class<final><computes>(editable):

```
        # Show the button that allows locking the vector aspect ratio.

```verse
        ShowPreserveRatio<public>:logic = external {}


```
        # Show the button that allows normalizing the vector.

```verse
        ShowNormalize<public>:logic = external {}


```
        # The minimum value allowed for each vector element.

```verse
        MinComponentValue<public>:?t = external {}


```
        # The maximum value allowed for each vector element.

```verse
        MaxComponentValue<public>:?t = external {}


```
        # The amount the slider moves for each step.

```verse
        SliderDelta<public>:?t = external {}


```
        # Used to scale a slider exponentially. Common values are found within the range of 1-20.

```verse
        SliderExponent<public>:?t = external {}


```
        # Used to change how sensitive the field value is when moving the slider via mouse cursor.

```verse
        MouseLinearDeltaSensitivity<public>:float = external {}

        MouseShiftMovePixelPerDelta<public>:float = external {}

    @attribscope_class
    @attribscope_struct
    @attribscope_data
    @customattribhandler
    editable_vector_number<public>(t:type) := class<final><computes>(editable):

```
        # Show the button that allows locking the vector aspect ratio.

```verse
        ShowPreserveRatio<public>:logic = external {}


```
        # Show the button that allows normalizing the vector.

```verse
        ShowNormalize<public>:logic = external {}


```
        # The minimum value allowed for each vector element.

```verse
        MinComponentValue<public>:?t = external {}


```
        # The maximum value allowed for each vector element.

```verse
        MaxComponentValue<public>:?t = external {}


```
        # Snap the spinbox to the nearest delta.

```verse
        SpinBoxDelta<public>:?t = external {}

    @attribscope_class
    @attribscope_struct
    @attribscope_data
    @customattribhandler
    editable_container<public> := class<final><computes>(editable):

```
        # If true, allows reordering of the container elements in the editor.

```verse
        AllowReordering<public>:logic = external {}


    agent<native><public> := class<unique><epic_internal>:

    localizable_agent<native><epic_internal> := class(localizable_value):

    (/Verse.org/Simulation:)MakeLocalizableValue<epic_internal>(Agent:agent):localizable_agent = external {}

    player<native><public> := class<unique><persistent><module_scoped_var_weak_map_key><epic_internal>(agent):

```
        # Succeeds when this `player` may be used as a module-scoped `var` `weak_map` key. This coincides with the corresponding player having joined the game and not yet left. Using a `player` as a module-scope `var` `weak_map` key when this method fails results in a runtime error.

```verse
        IsActive<native><public>()<reads><decides>:void


```
    # Type for which there is a single instance per round.  Use `GetSession` to get the current round's `session` instance. May be used with `weak_map` to implement global variables.
    # Note: may be changed in a future release to a single instance per game. Round-local behavior should not be relied upon.

```verse
    session<native><public> := class<unique><module_scoped_var_weak_map_key><epic_internal>:


```
    # Returns the `session` corresponding to the current round.  The result can be used with `weak_map` to implement global variables.
    # Note: may be changed in a future release to return a single instance per game. Round-local behavior should not be relied upon.

```verse
    GetSession<native><public>()<reads>:session


```
    # Waits specified number of seconds and then resumes. If `Seconds` = 0.0 then it waits until next tick/frame/update. If `Seconds` = Inf then it waits forever and only calls back if canceled - such as via `race`. If `Seconds` < 0.0 then it completes immediately and does not yield to other aysnc expressions.
    # Waiting until the next update (0.0) is especially useful in a loop of a coroutine that needs to do some work every update and this yields to other coroutines so that it doesn't hog a processor's resources.
    # Waiting forever (Inf) will have any expression that follows never be evaluated. Occasionally it is desireable to have a task never complete such as the last expression in a `race` subtask where the task must never win the race though it still may be canceled earlier.
    # Immediately completing (less than 0) is useful when you want programmatic control over whether an expression yields or not.

```verse
    Sleep<native><public>(Seconds:float)<suspends>:void


```
    # Get the seconds that have elapsed since the world began simulating

```verse
    GetSimulationElapsedTime<native><public>()<transacts>:float

    team<native><public> := class<unique><epic_internal>:


```

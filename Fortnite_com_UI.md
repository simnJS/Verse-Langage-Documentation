
```verse
(/Fortnite.com:)UI := module:

```
# Button with text message common base class. Displays a button with a custom message string.

```verse
    text_button_base<native><public> := class<abstract><epic_internal>(widget):

```
        # The text to display to the user. Used only during initialization of the widget and not modified by SetText.

```verse
        (/Fortnite.com/UI/text_button_base:)DefaultText<localizes><native><public>:message = external {}


```
        # Subscribable event that fires when the button is clicked.

```verse
        OnClick<public>():listenable(widget_message) = external {}


```
        # Sets the text displayed in the widget.

```verse
        SetText<native><public>(InText:message):void


```
        # Gets the text currently in the widget.

```verse
        GetText<native><public>():string


```
    # Text button with big and loud styling applied.

```verse
    button_loud<native><public> := class<final>(text_button_base):


```
    # Text button with normal styling applied.

```verse
    button_regular<native><public> := class<final>(text_button_base):


```
    # Text button with quiet styling applied.

```verse
    button_quiet<native><public> := class<final>(text_button_base):

    @deprecated

```
    # Deprecated. This function affects all players. Please use `fort_playspace.GetHUDController().ShowElements()`.
    # Shows a set of HUD elements.

```verse
    (PlayerUI:player_ui).ShowHUDElements<native><public>(HUDElements:[]hud_element_identifier):void

    @deprecated

```
    # Deprecated. This function affects all players. Please use `fort_playspace.GetHUDController().HideElements()`.
    # Hides a set of HUD elements.

```verse
    (PlayerUI:player_ui).HideHUDElements<native><public>(HUDElements:[]hud_element_identifier):void

    @deprecated

```
    # Deprecated. This function affects all players. Please use `fort_playspace.GetHUDController().ResetElementVisibility()`.
    # Resets the visibility for a set of HUD elements.

```verse
    (PlayerUI:player_ui).ResetHUDElementVisibility<native><public>(HUDElements:[]hud_element_identifier):void


```
    # A HUD controller that allows for showing and hiding of HUD elements.

```verse
    fort_hud_controller<native><public> := interface<epic_internal>:

```
        # Shows a set of HUD elements for every player. Note: This can be overridden by rules set by 'ForPlayer' functions since player specific rules are prioritized over general rules.

```verse
        ShowElements<public>(HUDElements:[]hud_element_identifier):void


```
        # Hides a set of HUD elements for every player. Note: This can be overridden by rules set by 'ForPlayer' functions since player specific rules are prioritized over general rules.

```verse
        HideElements<public>(HUDElements:[]hud_element_identifier):void


```
        # Resets the visibility for a set of HUD elements for every player. Note: This will not clear player specific rules set by the 'ForPlayer' functions which can only be reset by calling 'ResetElementsForPlayer'.

```verse
        ResetElementVisibility<public>(HUDElements:[]hud_element_identifier):void


```
        # Shows a set of HUD elements for a single player. Note: This overrides general rules set by non-player functions for the given elements. Call 'ResetElementsForPlayer' in order to return the player to general behavior

```verse
        ShowElementsForPlayer<public>(Player:player, HUDElements:[]hud_element_identifier):void


```
        # Hides a set of HUD elements for a single player. Note: This overrides general rules set by non-player functions for the given elements. Call 'ResetElementsForPlayer' in order to return the player to general behavior

```verse
        HideElementsForPlayer<public>(Player:player, HUDElements:[]hud_element_identifier):void


```
        # Resets the player-specific visibility rules of a set of HUD elements for a single player. Note: This will not reset rules that have been set by means other than the 'PerPlayer' functions.

```verse
        ResetElementsForPlayer<public>(Player:player, HUDElements:[]hud_element_identifier):void


```
    # Get the `fort_hud_controller` for the current `fort_playspace`.

```verse
    (Playspace:fort_playspace).GetHUDController<native><public>():fort_hud_controller

    creative_hud_identifier_all<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_build_menu<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_crafting_resources<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_elimination_counter<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_equipped_item<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_experience_level<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_experience_supercharged<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_experience_ui<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_health<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_health_numbers<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_hud_info<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_interaction_prompts<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_map_prompts<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_mimimap<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_minimap<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_pickup_stream<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_player_count<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_player_inventory<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_round_info<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_round_timer<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_shield_numbers<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_shileds<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_shields<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_storm_notifications<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_storm_timer<public> := class<final>(hud_element_identifier):

    creative_hud_identifier_team_info<public> := class<final>(hud_element_identifier):

    player_hud_identifier_all<public> := class<final>(hud_element_identifier):

    hud_identifier_world_resource_wood<public> := class<final>(hud_element_identifier):

    hud_identifier_world_resource_stone<public> := class<final>(hud_element_identifier):

    hud_identifier_world_resource_metal<public> := class<final>(hud_element_identifier):

    hud_identifier_world_resource_permanite<public> := class<final>(hud_element_identifier):

    hud_identifier_world_resource_gold_currency<public> := class<final>(hud_element_identifier):

    hud_identifier_world_resource_ingredient<public> := class<final>(hud_element_identifier):

    hud_identifier_visual_sound_effect_weapons<public> := class<final>(hud_element_identifier):

    hud_identifier_visual_sound_effect_loot<public> := class<final>(hud_element_identifier):

    hud_identifier_visual_sound_effect_movement<public> := class<final>(hud_element_identifier):

    hud_identifier_visual_sound_effect_vehicle<public> := class<final>(hud_element_identifier):

    hud_identifier_visual_sound_effect_healing<public> := class<final>(hud_element_identifier):

    hud_identifier_visual_sound_effect_all<public> := class<final>(hud_element_identifier):


```
    # Used to identify a HUD element.

```verse
    hud_element_identifier<native><public> := class<abstract><epic_internal>:


```
    # Slider with a text value. Displays a slider, its progress bar and value.

```verse
    slider_regular<native><public> := class<final>(widget):

```
        # The value to display to the user. Used only during initialization of the widget and not modified by SetValue.

```verse
        DefaultValue<native><public>:float = external {}


```
        # The minimum value that the slider can haver. Used only during initialization of the widget and not modified by SetMinValue.

```verse
        DefaultMinValue<native><public>:float = external {}


```
        # The maximum value that the slider can haver. Used only during initialization of the widget and not modified by SetMaxValue.

```verse
        DefaultMaxValue<native><public>:float = external {}


```
        # The amount to adjust the value by, when using a controller or keyboard. Used only during initialization of the widget and not modified by SetStepSize.

```verse
        DefaultStepSize<native><public>:float = external {}


```
        # Sets the value of the slider, will clamp the value to be within the sliders minimum and maximum value.

```verse
        SetValue<native><public>(InValue:float):void


```
        # Gets the value of the slider.

```verse
        GetValue<native><public>():float


```
        # Sets the minimum value of the slider, will enforce that the sliders maximum value is always larger than or equal to the minimum value.

```verse
        SetMinValue<native><public>(InMinValue:float):void


```
        # Gets the minimum value of the slider.

```verse
        GetMinValue<native><public>():float


```
        # Sets the maximum value of the slider, will enforce that the sliders maximum value is always larger than or equal to the minimum value.

```verse
        SetMaxValue<native><public>(InMaxValue:float):void


```
        # Gets the maximum value of the slider.

```verse
        GetMaxValue<native><public>():float


```
        # Sets the amount to adjust the value by, when using a controller or keyboard.

```verse
        SetStepSize<native><public>(InValue:float):void


```
        # Gets the amount to adjust the value by.

```verse
        GetStepSize<native><public>():float


```
        # Subscribable event that fires when the value of the slider has changed.

```verse
        OnValueChanged<public>():listenable(widget_message) = external {}


```
    # Text block widget. Displays text to the user.

```verse
    text_block<native><public> := class<final>(text_base):

```
        # The direction the shadow is cast. Used only during initialization of the widget and not modified by SetShadowOffset.

```verse
        DefaultShadowOffset<native><public>:?vector2 = external {}


```
        # The color of the shadow. Used only during initialization of the widget and not modified by SetShadowColor.

```verse
        DefaultShadowColor<native><public>:color = external {}


```
        # The opacity of the shadow. Used only during initialization of the widget and not modified by SetShadowOpacity.

```verse
        DefaultShadowOpacity<native><public>:type {_X:float where 0.000000 <= _X, _X <= 1.000000} = external {}


```
        # Sets the direction the shadow is cast.

```verse
        SetShadowOffset<native><public>(InShadowOffset:?vector2):void


```
        # Gets the direction the shadow is cast.

```verse
        GetShadowOffset<native><public>():?vector2


```
        # Sets the color of the shadow.

```verse
        SetShadowColor<native><public>(InColor:color):void


```
        # Gets the color of the shadow.

```verse
        GetShadowColor<native><public>():color


```
        # Sets the opacity of the shadow.

```verse
        SetShadowOpacity<native><public>(InOpacity:type {_X:float where 0.000000 <= _X, _X <= 1.000000}):void


```
        # Gets the opacity of the shadow.

```verse
        GetShadowOpacity<native><public>():type {_X:float where 0.000000 <= _X, _X <= 1.000000}

using {/Verse.org/Assets}
using {/Fortnite.com/AI}
using {/Verse.org/Native}
using {/Verse.org/Simulation/Tags}
using {/Fortnite.com/Game}
using {/Verse.org/SceneGraph}


```

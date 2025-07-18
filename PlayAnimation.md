
```verse
PlayAnimation := module:

```
# Result of a PlayAndAwait request.

```verse
        play_animation_result<native><public> := enum:

```
            # The animation completed successfully.

```verse
            Completed

```
            # The animation was interrupted whilst playing.

```verse
            Interrupted

```
            # The animation encountered an error during initialization or whilst playing.

```verse
            Error


```
        # An interface for playing an animation on an object.

```verse
        play_animation_controller<native><public> := interface<epic_internal>:

```
            # Play an animation sequence.

```verse
            PlayAndAwait<public>(AnimationSequence:animation_sequence, ?PlayRate:float = external {}, ?PlayCount:float = external {}, ?StartPositionSeconds:float = external {}, ?BlendInTime:float = external {}, ?BlendOutTime:float = external {})<suspends>:play_animation_result


```
            # Start an animation sequence and obtain an instance to query and manipulate.

```verse
            Play<public>(AnimationSequence:animation_sequence, ?PlayRate:float = external {}, ?PlayCount:float = external {}, ?StartPositionSeconds:float = external {}, ?BlendInTime:float = external {}, ?BlendOutTime:float = external {}):play_animation_instance


```
        # An animation instance created from play_animation_controller.Play that can be queried and manipulated.

```verse
        play_animation_instance<native><public> := class<epic_internal>:

```
            # Returns the state of the animation playback.

```verse
            GetState<native><public>()<transacts>:play_animation_state


```
            # Stops the animation.

```verse
            Stop<native><public>():void


```
            # Event triggered when the animation is completed.

```verse
            CompletedEvent<native><public>:listenable(tuple()) = external {}


```
            # Event triggered when the animation is interrupted.

```verse
            InterruptedEvent<native><public>:listenable(tuple()) = external {}


```
            # Event triggered when the animation has finished to blend out.

```verse
            BlendedInEvent<native><public>:listenable(tuple()) = external {}


```
            # Event triggered when the animation is beginning to blend out.

```verse
            BlendingOutEvent<native><public>:listenable(tuple()) = external {}


```
            # Helper function that waits for the animation to complete or be interrupted.

```verse
            Await<public>()<suspends>:play_animation_result = external {}


```
            # Helper function that succeeds if the state is Playing, BlendingIn, or BlendingOut.

```verse
            IsPlaying<public>()<transacts><decides>:void = external {}


```
        # The potential states of a play animation instance.

```verse
        play_animation_state<native><public> := enum:

```
            # The animation is blending in.

```verse
            BlendingIn

```
            # The animation has blended in, is playing, and has not begun blending out.

```verse
            Playing

```
            # The animation is playing and is blending out.

```verse
            BlendingOut

```
            # The animation completed successfully.

```verse
            Completed

```
            # The animation was stopped internally.

```verse
            Stopped

```
            # The animation was interrupted externally.

```verse
            Interrupted

```
            # An error occurred at creation or during playback.

```verse
            Error


```
        # Get the play_animation_controller for the specified character.

```verse
        (InCharacter:fort_character).GetPlayAnimationController<native><public>()<transacts><decides>:play_animation_controller


```

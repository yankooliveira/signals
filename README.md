# Signals
### A typesafe, lightweight messaging lib for Unity.
---
Inspired by StrangeIOC, minus the clutter.
Originally based on [CSharpMessenger](http://wiki.unity3d.com/index.php/CSharpMessenger_Extended).
Converted to use strongly typed parameters and prevent use of strings as ids.

Special thanks to Max Knoblich for code review and Aswhin Sudhir for the anonymous function asserts suggestion.

Supports up to 3 parameters (more than that, and you should probably use a specialized VO as a single parameter).
You can read about the reasons behind it [on my blog](http://yankooliveira.com/index.php/2018/01/15/signals).

### Usage:
1) Define your signal with up to 3 payload parameters, eg:
```c#
public class EndGameSignal : ASignal {}
public class ScoreSignal : ASignal<string, int> {}
```
2) Add listeners on portions that should react, eg on Awake():
```c#
Signals.Get<ScoreSignal>().AddListener(OnScore);
```
3) Dispatch, eg:
```c#
Signals.Get<ScoreSignal>().Dispatch(playerName, playerScore);
```
4) Don't forget to remove the listeners upon destruction! Eg on OnDestroy():
```c#
Signals.Get<ScoreSignal>().RemoveListener(OnScore);
```
5) You also have your local Signal Hub that is specific to a given object instead of using the global one. The syntax is exactly the same.
```c#
SignalHub playerSignals = new SignalHub();
playerSignals.Get<ScoreSignal>().Dispatch(playerName, playerScore);
```


Hit me up on [twitter](https://twitter.com/yankooliveira) for any suggestions or questions.

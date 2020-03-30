# debouncer

Tap debounce simplifying widget

## Instruction

Assume your code with some button look like this:

```dart
//...
child: RaisedButton(
  color: Colors.blue,
  disabledColor: Colors.grey,
  onPressed: () async => await someLongOperation(),
  child: const Text('Short'),
  );
//...
```

and you do not want user to be able to press the button again several times and start other 
someLongOperation functions. Example is a Navigator pop function - it can take a few hundred of 
millis to navigate and user can press the button several times, and that will lead to undesired pop 
several screens back instead of one.

Wrap this code to Debouncer and move RaisedButton onPressed contents to Debouncer onTap:

```dart
//...
child: Debouncer(
  onTap: () async => await someLongOperation(),
  builder: (BuildContext context, DebouncerOnTap onTap) {
    return RaisedButton(
      color: Colors.blue,
      disabledColor: Colors.grey,
      onPressed: onTap,
      child: const Text('Short'),
    );
  },
),
//...
```

Debouncer will disable the RaisedButton by settings onPressed to null while onTap is being executed. 

You can add optional delay to be sure that the button is disabled some time after someOperation is 
called.


```dart
//...
onTap: () async {
    someOperation();
    
    // optional
    await Future<void>.delayed(
      const Duration(milliseconds: 1000),
      () {},
    );
},
//...
```

See example application for details:

![](/page/debounced.gif)

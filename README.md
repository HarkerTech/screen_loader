# screen_loader

Using `showDialog` for showing loader is a **BAD IDEA**. You may end up messing the navigation stack and `context` due to pushing and popping the loader(dialog). Hence, I have come up with an easy to use mixin `ScreenLoader`, which will handle the loading on the screen. You can customise the loading as well, check below how it is done.

## Important
Replace your `build(BuildContext context)` function with `screen(BuildContext context)`

```dart
@override
Widget screen(BuildContext context) {
  return Scaffold(
    appBar: _buildAppBar(),
    body: _buildBody(),
  );
}
```

## Basic Usage

Extend your screen(`StatefulWidget`) with `ScreenLoader`. Use `performFuture` to show loader while your future us being performed. That's it!

<img src="https://raw.githubusercontent.com/arnold-parge/screen_loader/master/example/basic.gif" width="250" />

## Override Loader

Simply overide `loader()` method in your `_ScreenState` class

```
loader() {
    // here any widget would do
    return AlertDialog(
        title: Text('Wait.. Loading data..'),
    );
}
```

<img src="https://raw.githubusercontent.com/arnold-parge/screen_loader/master/example/local.gif" width="250" />

## Override Loader Gobally

```dart
void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ScreenLoaderApp(
      app: MaterialApp(
        title: AppStrings.yapChat,
        theme: ThemeData(
          primarySwatch: Colors.blue,
        ),
        home: Screen(),
      ),
      globalLoader: AlertDialog(
        title: Text('Gobal Loader..'),
      ),
    );
  }
}

```

<img src="https://raw.githubusercontent.com/arnold-parge/screen_loader/master/example/global.gif" width="250" />

## Priority of loaders

- **Local loader**: the one you override in the `_ScreenState` class
- **Global loader**: the one you specify in `ScreenLoaderApp`. Note: if you don't override `local()`, this loader will be used.
- **Default loader**: if you don't specify global loader or override local loader, this loader will be used

### PS 
- PRs are welcome
- Please raise issues on https://github.com/arnold-parge/screen_loader.
- Open for suggestions ❤️
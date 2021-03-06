# Flutter
- a cross platform
- strongly typed
- mostly OOP
- hybrid app framework

## Architecture
- layers
    - framwork: the UI framework
    - engine: skia (based on C++)
    - embedder: adapt to different OS
- compile modes
    - JIT mode: patch code to dart VM dynamically
    - AOT mode: compiles to assembly using custom protocol

## The Good 
- dev experience
    - same code base for multiple platforms
    - fast iteration: stateful hot reload
- performance
    - directly compiled to machine code
    - does not rely on native ui primitive
        - no need for bridging (composite the entire screen at once)
        - completely decoupled from OS native behaviour
    - fluid animation
    - efficient layout & paint
    	- split-phase: layout + size 
        - done in one-pass: down, then up
        - complexity: O(n)
- declarative UI
    - state driven
    - framework handles rerender
- design
    - consistent cross-platform design & behaviours
    - more customizable
    - use simple constraints-based layout system (compare to iOS)
        - min/max width and height


## The Ugly
- hot patch
    - hard to patch code dynamically (due to AOT)
- widget
    - Tab is hardcoding the height
    - `popup`, `dialogs`, `modal` depends on route
    - localization requires context
- testing
    - widget testing is awkward
        - pumpAndSettle doesn't always work (animation may never settle)
    - some test require random amount of pumps

## The Bad
- native + flutter support is not mature yet
- hard to do fine grained widget level error handling
- Cupertino Switch color cannot be controlled through themes
- loading image assets
	- can not load nested directories
	- no svg support
- intellij editor
    - cannot connect with Flutter inspector 
	    - must disable devtools in the flutter section of the editor
- no storybook to showcase design
- limitations of hot reload
    - changes made out side `build()` will not be applied
    - newly added static field will not be applied
    - change to widget root will not be applied
    - changes in lifecycle methods will not be applied

## Why Dart as the programming language
- JIT: fast dev cycles
- AOT: good performance in production (compile to ARM code)
    - high performance
    - low latency
- tree shaking compiler
- Dart is optimized for Flutter
    - support AOT because of Flutter
    - Dart VM optmize for latency (instead of throughput) for Flutter
- OOP
    - industry has mature solution
- strong types
- fast memory allocations
    - functional-style flow favors small short-lived memory allocations
    - generational garbage collection
- easy to learn (like JS & Java)

## Dart Limitations
- no function overloading

## UI (the three widget trees)
- UI consists ofthree trees: Widgets, Elements and RenderObjects
- widget: configure
	- configuration of the widget (in the general sense)
	- hold properties (e.g. amount of padding, reference to child)
	- offer public API
- element: manage
	- hold a spot in the UI hierachy
	- manage lifecycle
	- manage parent/child relation
- renderObject: paint
	- size
	- paint
	- layout children
	- claim input events

## widget
- immutable description (configuration) of view
- optimized for rebuild
- implementation
    - types of widget
        - `RenderObjectWidget`
        - `SingleChildObjectWidget`
        - `LeafRenderObjectWidget`
    - create element
        - `createElement()`
            - `SingleChildObjectWidget`
            - `LeafRenderObjectElement`
    - `canUpdate` method
        - check if `key` and `runtimeType` change
        - if no change, update widget only & reuse `element` & `renderObject`
    - add debug info to devtool
        - `debugFillProperties`

## Element
- hold a spot in the UI hierachy
    - keep track of widgets' positions
    - keep track of RenderObjects
- manage lifecycle
- manage parent/child relation
- implementation
    - types of element
        - RenderObjectElement
        - LeafRenderObjectElement
    - create renderObject
        - `mount`: `createRenderObject`

## RenderObjects
- size
- paint
- layout children
- claim input events


## UI init mechanism
- attach root widget & warmup
    WidgetsFlutterBinding.ensureInit
	    attach root widget
	    warmup
- build the trees
    - widget tree
    - element tree
    - renderObject tree

## UI rebuld mechanism
- trigger rebuild through setState
- check `canUpdate` to reuse renderObject 
    - if runtimetype & key stays the same
        - replace the old widget with a new one
        - element updates renderObject with the new config

## state management
- provider pattern
    - data model
        - store state
        - can notify changes
            - `notifyListener()`
        - `ChangeNotifier`
    - provider
        - expose data to subtree
        - `ChangeNotifierProvider`
    - consumer
        - subscribe to changes in provider
        - `Consumer`

## The rendering pipeline
- User Input
- Animation	
- Build
- layout
- paint
- composite
- rasterize
- GPU

### From Widget to Image
- use Flutter's golden test mechanism as an example
- steps
    - rendering
        - get the renderObject's first parent renderObject that is a RepaintBoundary
        - get the widget's renderObject: finder -> element -> renderObject
        - get offsetLayer from renderObject
        - convert offsetLayer to scene
    - composite & rasterize
        - scene to image (native call)


## Navigation


### Annoynoumous Route
```dart
onPressed: () {
    Navigator.push(
        context,
        MaterialPageRoute(builder: (context) {
        return DetailScreen();
        }),
    );
}
```

### Named Route

define route map
```dart
return MaterialApp(
    routes: {
        '/': (context) => HomeScreen(),
        '/details': (context) => DetailScreen(),
    },
);
```

push route using name
```dart
onPressed: () {
    Navigator.pushNamed(
        context,
        '/details',
    );
}
```


### generative route

```dart
onGenerateRoute: (settings) {
  // Handle '/'
  if (settings.name == '/') {
    return MaterialPageRoute(builder: (context) => HomeScreen());
  }
  
  // Handle '/details/:id'
  var uri = Uri.parse(settings.name);
  if (uri.pathSegments.length == 2 &&
      uri.pathSegments.first == 'details') {
    var id = uri.pathSegments[1];
    return MaterialPageRoute(builder: (context) => DetailScreen(id: id));
  }
  
  return MaterialPageRoute(builder: (context) => UnknownScreen());
},
```

### declarative routing (Navigator 2.0 API)
- use app state to control screens
- page: immutable objects
- router: list of pages displayed by the Navigator
- RouteInformationProvider: provide route info
- RouteInformationParser: parse route info into custom data type
- RouterDelegate:
    - defines how to receive state change
    - how to respond to state change
    - listen to RouteInformationParser
    - build Navaigator with current pages
- BackButtonDispatcher: reports back button press to Router

## Flutter lifecycle
- initState: (called before render)
    - must not call setState (as the widget hasn't been mounted)
	- react: didMount (called after render)
- didUpdateWidget (called before render)
	- react: didUpdate (called after render)
- didChangeDependencie 
	- react: willReceiveProps
- dispose (willUnmount)

## MVVM architecture
- view: show things
    - the UI widgets
    - `Consumer`
- viewModel: 
    - presentation logic
    - `Provider`
- model: 
    - service
    - store


## BLOC Architecture

### Flutter Bloc Integration
- use provider underneath
- code constructs
    - Bloc: map events to streams
        - from view: receive events
            - act as **sink**: receive value over time
        - for view: 
            - act as **stream**: yeild multiple values over time
            - map events to states (stream)
            - request data
    - BlocBuilder: consumes bloc and returns a widget
    - BlocProvider: provide a bloc instance to the subtree

### The three layers of Bloc
- presentation
- business logic
- Data
	- data provider
	- repository

### data provider layer
- provides raw data
- contains CRUD operations

```dart
class DataProvider {
    Future<RawData> readData() async {
        // Read from DB or make network request etc...
    }
}
```

### data repository layer
- wrapper of data provider(s)
- talks to the bloc layer

```dart
class Repository {
    final DataProviderA dataProviderA;
    final DataProviderB dataProviderB;

    Future<Data> getAllDataThatMeetsRequirements() async {
        final RawDataA dataSetA = await dataProviderA.readData();
        final RawDataB dataSetB = await dataProviderB.readData();
        return _filterData(dataSetA, dataSetB);
    }
}
```

### BLOC layer
- full name: Bussiness Logic component
- stores business logic
- receives event from UI
- retrieve data from data provider to build state
- provide state (as Stream) for UI
- an interface built around Dart Stream
- everything is a stream of events
	- widgets submit events
	- other widgets will respond
	- BLoC sits in the middle, managing the conversation
	- dart has default support for working with syntaxs

```dart
class BusinessLogicComponent extends Bloc<MyEvent, MyState> {
    final Repository repository;

    Stream mapEventToState(event) async* {
        if (event is AppStarted) {
            try {
                final data = await repository.getAllDataThatMeetsRequirements();
                yield Success(data);
            } catch (error) {
                yield Failure(error);
            }
        }
    }
}
```

### Bloc to Bloc communication
- every block contains a state stream
- block subscribes to state in another block

```dart
class MyBloc extends Bloc {
  final OtherBloc otherBloc;
  StreamSubscription otherBlocSubscription;

  MyBloc(this.otherBloc) {
    otherBlocSubscription = otherBloc.listen((state) {
        // React to state changes here.
        // Add events here to trigger changes in MyBloc.
    });
  }

  @override
  Future<void> close() {
    otherBlocSubscription.cancel();
    return super.close();
  }
}
```

### presentation layer
- render based on bloc states
- handle user input and lifecycle events

```dart
class PresentationComponent {
    final Bloc bloc;

    PresentationComponent() {
        bloc.add(AppStarted());
    }

    build() {
        // render UI based on bloc state
    }
}
```


## Error handling
- runZoneGuarded
    - create an error zone that wraps the app
- isolate.current.addErrorListener: 
	- any errors that may occur within the entry function
- FlutterError.onError
	- layout exceptions (e.g. overflow)
	- anything uncaught during widget build

## themeing
- Color Theme
    - PrimarySwatch
- Text Theme
- Theme for individual Widget

## layout mechanism
- principles
    - constraints go down: propagate from parent to children
    - sizes go up: from child to parent
    - position set by parent: each widget cannot determine its own position
- constraints
    - as big as possible: `Container`, `Center`, `ListView`
    - just wrap children: `Transform`, `Opacity`
    - particular size: `Image`, `Text`
    - depend on contraints given (flex boxes): `Column`, `Row`
        - cross direction (horizontal for `column`) must be bounded
- concepts
    - tight vs losse
        - tight: child must be of certain size (e.g. screen -> center)
        - loose: child smaller than certain size (e.g. center -> child)

## design system
- use logical pixel (aka. density-independent pixel)
- pixel mapped to a fixed physical width (1 logical pixel ~= 38px)

## layout widgets
- single child
    - `Center`
    - `Container`
- multi child
    - `row`
        - variant `ListTile`
    - `column`
        - variant `ListView`
    - `ListView`
    - `Stack`

## responsive design
- `LayoutBuilder`
- `MediaQuery.of(context)
- AspectRatio
- CustomSingleChildLayout
- CustomMultiChildLayout
- FittedBox
- FractionallySizedBox
- LayoutBuilder
- MediaQuery
- MediaQueryData
- OrientationBuilder`


## animations
- drawing based animations:
    - generate using 3rd party tools
    - import into Flutter
- code-based animations: use Flutter
    - implicit
        - tweak existing widgets 
        - built-in widgets
            - `AnimatedContainer`
            - other `AnimatedXxx`
        - TweenAnimationBuilder
            - custom implicit animation
    - explicit
        - can control animation timing (`AnimationController`)
        - must manage lifecycle manually
        - built-in widgets
            - `XxxTransition`
            - AnimatedWidget
            - AnimatedBuilder
            - CustomPainter (use only for extreme performance optimization)
        - use cases: 
            - repeating animations
            - discountinous animations
            - animations involing multiple widgets


## performance optimization
- shader compilation jank
	- use sksl warmup

## performance monitoring
- performance issue should be debugged in profile mode
- devtool
    - performance overlay
    - widget rebuild tracker
    - memory tab
- enable skia-level tracing
    - `flutter run --profile --trace-skia`

## Threading model
- platform thread: native plugin code
- UI thread
	- Dart code + Flutter framework code
	creates a layer tree: a lightweight object containing painting commands - (device-independent)
- raster thread
	- skia engine
	- prepare data for GPU
- I/O thread
	- expensive I/O tasks

## widgets overview
- safearea
    - adapt stange physical device shape
	- use MediaQuery behind the scenes
- expanded
	- make child take all available space
	- inflexible objects are layout first
	- `flex` param to distribute space by ratio
- wrap
	- wrap child when overflow
	- replace row
	- support alignment, direction, spacing
- AnimatedContainer
	- implicit animation on state change
- Opacity
	- hide the widget while keeping the space
	- stack images with different opacity
	- AnimatedOpacity support opacity change
- FutureBuilder
	- return widget based on the state of a future
- FadeTransition
	- fade a tranistion in and out
- FloatingActionButton
	- can be embedded in the bottom navigation bar
- PageView
	- make pages scrollable
	- PageController: swipe detection, animation, set initial page
- Table
	- non-scrollable grid layout
- SliverAppBar
	- animated header that reacts to scroll
	- used with CustomScrollView to provide finer-grained control
	- control how app bar is expanded when scroll up, if should reappear when scroll down
- FadeInImage
	- placeholder for network image
- StreamBuilder
    - processing streams
- InheritedWidget
    - give subtree widget access to top of the widget tree
- ClipRRect
    - give round corners
- Hero
    - transition between routes while keep focus on a wdiget  
- CustomPaint
    - low level canvas-like widget
- tooltips
    - show tooltip
    - privide accessiblity on press
- FitBox
    - fit a box into another
    - adjustable through fit, align
- LayoutBuilder
    - return widget according to constraints
- AbsorbPointer
    - aborb touch events
- Transform
    - transform widget or entire app
- Image Filter
    - used inside BackdropFilter
    - affects objects beneath the filter
- Align
    - align child in ints parent
- Positioned
    - absolute position an element inside a stack
- AnimatedBuilder
    - control animation   
- Dismissiable
    - emulate swipe to delete
- SizedBox
    - add size contraint to a child   
- ValueListenableBuilder  
    - used together with valueNotifier (maybe use provider instead)
- Draggable
    - drag things
- AnimatedList
    - make list change look more natural
- Flexible
    - distribute space based on flex
    - set fit to loose will use child's preferred size
- MediaQuery
    - check device info and preferences
- Spacer
    - customize space between widgets (compare to AxisAlignment)
- AnimatedIcons
    - make icon play animation
- AspectRatio
    - enforce child widget aspect ratio
- LimitedBox
    - gives child a default size when the parent is unbounded
- Placeholder
    - stand in for actual widget
- RichText
    - style some part of text
- ReorderableListView
    - reorderable list view
- AnimatedSwitcher    
    - switch between two widgets
- DeviceInfo
    - get physical device info
- AnimatedPadding
    - animate padding change
- Indexed Stack
    - shows one widget a time, while preserving all widgets' state
- Semantics
    - add semantic meaning to widget
- ConstrainedBox
    - a container widget that sets max width and height
- Stack
    - stack child widgets on top of each other
- AnimatedOpacity
    - implicit fade in/ fade out animation
- FractionallySizedBox
    - size box according to screen width (widthFactor, heightFactor)
- ListView
    - shows a list of items
- ListTile
    - item following material design guideline
- Container
    - equivalent to div
- SelectableText
    - like text, but make text selectable
- DataTable
    - auto size column based on data
- Slider
    - input element for rating stuff
    - slider.adaptive show differently for different platforms
- AlertDialog
    - a dialog for yes / no
- AnimatedCrossFade
    - a widget fade into another
- DraggableScrollableSheet
    - draggle things out, then scroll on it
- ColorFiltered
    - add a color filter on top of the widget
- ToggleButtons
    - a group of buttons, with one of the selected
- CupertinoActionSheet
    - an actionsheet
- TweenAnimationBuilder
    - build custom animation
- Image
    - show image from assets, network
    - loadingBuilder can show image load progress 
    - set size to prevent jumps
    - fill: stretch
    - cover: clip
- IgnorePointer
    - ignore the current element in hit test
    - will hit the element below the current element when press
- Drawer
    - a navigation drawer
    - commonly used together with ListView and ListTile
- SnackBar
    - a toast at the bottom of the screen
    - used together with Scaffold.of(context)
- ListWheelScrollView 
    - list view placed on a wheel, scroll rotates the wheel
- ShaderMask
    - apply gradient or image to a widget
- NotificationListener    
    - catch notifactions (e.g. scroll notifcation) bubbling up to the ancestors
- Builder
    - provides complete context without a build method
- ClipPath
    - like ClipRRect, but with custom path
- CircularProgressIndicator
    - use circle to indicate progress
- LinearProgressIndicator
    - use line to indicate progress
- Divider
    - a visual line to seperate sections
- ClipOval
    - clip child to a circular/oval ship
- AnimatedWidget
    - abstract class for widgets with animation effect
- CheckBoxListTile
    - CheckBox + ListTile
- SwitchListTile
    - Switch + ListTile
- AboutDialog
    - a convient widget for showing legal stuff
- sqlflite
    - one of the sqllite package
- InteractiveViewer
    - limit a big widget in a view port
    - user can zoom & pan to see the entire widget
- GridView
    - show grid of items
- Location
    - get GPS location
- ImageFiltered
    - blur, rotation effect
- url_launcher
    - opening webpage, email, or SMS from the app
- ElevatedButton
	- onPrimary: text, icons, overlay color
	- primary: background fill
	- onSurface: **disabled** text, icon, fill color
- OutlinedButton
	- primary: text, icons, overlay, pressed colors, 
	- onSurface: **disabled** text, icon color
    - feedback: backgroundColor
- Device_info
    - get OS and device model info through system APIs
- PhysicalModel
    - create shadow underneath a box
    - takes no space
- Async 
    - StreamGroup: merge multiple streams into one
    - AsyncCache: give cached result within a time frame
    - StreamQueue: turn stream results into synchronous list of futures
- Scrollbar
    - show scroll position and scroll track for list view

## packages

### architecture
- MVVM utils: stacked
- dependency injection
  - get_it: service locator to provide object implmentation

### testing
- official
    unit test: flutter_test: widget test
    e2e test: flutter_driver: integration test
- mockito: mock & verify matcher
- network_image_mock

### state management
- provider: context-like state management
- event_bus: pub/subscribe pattern for decoupling application

### navigation
- url_launcher
- uni_links: deep link support

### Authentication
- flutter_appauth: connect with OAuth and OpenID connect

### network
- official
    - http: http request
- dio: wrapper over http
    - interceptors
- connectivity: get network status
- flutter_offline: handle offline
- system_proxy: easier to grab network request

### local storage
- sqflite
- shared_preferences
- flutter_secure_storage (encryted)
- hive (encrypted)

### utils
- rxdart
- json_annotation: JSON serialization/deserialization
- json_serializable: generate class to convert class to JSON
- flutter_launcher_icons: simplify updating app's launcher icons
- flutter_native_splash: simplify updating app's splash screen
- package_info: query version code
- intl: internationalization
- localize message
- date & number formatting
- clock: wrapper for clock api
- fake_async: test util for async functions
- email_validator: validate email
- built_value
    
### UI widgets
- flutter_slidable
- animated_text_kit
- dots_indicator: dot-based progress bar
- month_picker_dialog: md style date picker
    - loading_overlay: overlay for loading indicators
    - slider_button: just a button
- pin_code_text_field: enter a password
- webview_flutter: 
- bot_toast: custom toast
- dotted_border: add dotted border around widget
- flutter_svg: draw svg on widget
- infinite_scroll_pagination: infinite scroll
- auto_size_text: auto resize text to fit within bounds
- shimmer: skeleton screen effects
- CachedNetworkImage: automatic cache network image
- infinite_scroll_pagination
- animation: prebuilt animations
- flutter_svg: use svg in flutter

### assets
- cupertino_icons
- google_fonts: load font by http
- font_awesome_flutter

### analytics
- flutter_segment
- firebase_analytics：google analytics for apps

### config
- flutter_launcher_icons
- flutter_launcher_name

### build
- build_runner: dart code generator
- environment_config


### Notifications
- notification_permissions: check notification permission
- flutter_local_notifications

### Hardware
- sensors
- battery
- geolocator
- device_info
- just_audio
- package_info
- location
- path_provider	
- share

### lint
- offical
    - pedantic: a set of lint rules used by Google

### Service integration
- firebase_core
- firebase_messaging
- firebase dynamic link

## Android vs iOS behavior difference
- push a new page
    - android: push navigation: bottom to up 
    - ios: 
        - regular push page: horizontal
        - fullscreen modal: bottom to up
- back navigation
    - android: pop page by the back button of OS
    - ios: pop page by edge swipe
- overscroll 
    - android: show glow indicator
    - ios: snaps back
- return to top:
    - ios: click status bar return to top
- typography:
    - android: roboto
    - ios: san franciso
- haptic feedback
    - android: on field select -> vibrate and 'buzz' sound
    - ios: scrolling through picker items -> light impact sound

## Questions
- nullsafety
- why and how to use isolate
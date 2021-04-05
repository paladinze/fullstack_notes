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
- declarative UI
    - state driven
    - framework handles rerender
- design
    - consistent cross-platform design & behaviours

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
- shared_preferences
- flutter_secure_storage (encryted)
- hive (encrypted)

### utils
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
    
### UI widgets
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

### Hardware
- detect phone shake

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


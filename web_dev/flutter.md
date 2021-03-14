# Flutter

- a cross platform app framework
- strongly typed
- oop

## architecture
- compiles code to native code
- framwork
  - widgets
  - utils

## why 
- dev experience
    - stateful hot reload
- performance
    - directly compiled to machine code
    - does not use native ui primitive
        - no need for bridging (composite the entire screen at once)
        - completely decoupled from OS native behaviour
- declarative UI
    - state driven
    - framework handles rerender

## unit system
- use logical pixel (aka. density-independent pixel)
- pixel mapped to a fixed physical width (1 logical pixel ~= 38px)

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

## display widgets


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




animatedContainer
filled stacks channel
flare
List tile

SizedBox.expand

splash screen

Image.asset(
  'images/lake.jpg',
  fit: BoxFit.cover,
),




## widgets overview
safearea
	adapt stange physical device shape
	use MediaQuery behind the scenes
expanded
	make child take all available space
	inflexible objects are layout first
	`flex` param to distribute space by ratio
wrap
	wrap child when overflow
	replace row
	support alignment, direction, spacing
AnimatedContainer
	implicit animation on state change
Opacity
	hide the widget while keeping the space
	stack images with different opacity
	AnimatedOpacity support opacity change
FutureBuilder
	return widget based on the state of a future
FadeTransition
	fade a tranistion in and out
FloatingActionButton
	can be embedded in the bottom navigation bar
PageView
	make pages scrollable
	PageController: swipe detection, animation, set initial page
Table
	non-scrollable grid layout
SliverAppBar
	animated header that reacts to scroll
	used with CustomScrollView to provide finer-grained control
	control how app bar is expanded when scroll up, if should reappear when scroll down
FadeInImage
	placeholder for network image
StreamBuilder
    processing streams
InheritedWidget
    give subtree widget access to top of the widget tree
ClipRRect
    give round corners
Hero
    transition between routes while keep focus on a wdiget  
CustomPaint
    low level canvas-like widget
tooltips
    show tooltip
    privide accessiblity on press
FitBox
    fit a box into another
    adjustable through fit, align
LayoutBuilder
    return widget according to constraints
AbsorbPointer
    aborb touch events
Transform
    transform widget or entire app
Image Filter
    used inside BackdropFilter
    affects objects beneath the filter
Align
    align child in ints parent
Positioned
    absolute position an element inside a stack
AnimatedBuilder
    control animation   
Dismissiable
    emulate swipe to delete
SizedBox
    add size contraint to a child   
ValueListenableBuilder  
    used together with valueNotifier (maybe use provider instead)
Draggable
    drag things
AnimatedList
    make list change look more natural
Flexible
    distribute space based on flex
    set fit to loose will use child's preferred size
MediaQuery
    check device info and preferences
Spacer
    customize space between widgets (compare to AxisAlignment)
AnimatedIcons
    make icon play animation
AspectRatio
    enforce child widget aspect ratio
LimitedBox
    gives child a default size when the parent is unbounded
Placeholder
    stand in for actual widget
RichText
    style some part of text
ReorderableListView
    reorderable list view
AnimatedSwitcher    
    switch between two widgets
DeviceInfo
    get physical device info
AnimatedPadding
    animate padding change
Indexed Stack
    shows one widget a time, while preserving all widgets' state
Semantics
    add semantic meaning to widget
ConstrainedBox
    a container widget that sets max width and height
Stack
    stack child widgets on top of each other
AnimatedOpacity
    implicit fade in/ fade out animation
FractionallySizedBox
    size box according to screen width (widthFactor, heightFactor)
ListView
    shows a list of items
ListTile
    item following material design guideline
Container
    equivalent to div
SelectableText
    like text, but make text selectable
DataTable
    auto size column based on data
Slider
    input element for rating stuff
    slider.adaptive show differently for different platforms
AlertDialog
    a dialog for yes / no
AnimatedCrossFade
    a widget fade into another
DraggableScrollableSheet
    draggle things out, then scroll on it
ColorFiltered
    add a color filter on top of the widget
ToggleButtons
    a group of buttons, with one of the selected
CupertinoActionSheet
    an actionsheet
TweenAnimationBuilder
    build custom animation
Image
    show image from assets, network
    loadingBuilder can show image load progress 
    set size to prevent jumps
    fill: stretch
    cover: clip
IgnorePointer
    ignore the current element in hit test
    will hit the element below the current element when press
Drawer
    a navigation drawer
    commonly used together with ListView and ListTile
SnackBar
    a toast at the bottom of the screen
    used together with Scaffold.of(context)
ListWheelScrollView 
    list view placed on a wheel, scroll rotates the wheel
ShaderMask
    apply gradient or image to a widget
NotificationListener    
    catch notifactions (e.g. scroll notifcation) bubbling up to the ancestors
Builder
    provides complete context without a build method
ClipPath
    like ClipRRect, but with custom path
CircularProgressIndicator
    use circle to indicate progress
LinearProgressIndicator
    use line to indicate progress
Divider
    a visual line to seperate sections
ClipOval
    clip child to a circular/oval ship
AnimatedWidget
    abstract class for widgets with animation effect
CheckBoxListTile
    CheckBox + ListTile
SwitchListTile
    Switch + ListTile
AboutDialog
    a convient widget for showing legal stuff
sqlflite
    one of the sqllite package
InteractiveViewer
    limit a big widget in a view port
    user can zoom & pan to see the entire widget
GridView
    show grid of items
Location
    get GPS location
ImageFiltered
    blur, rotation effect
url_launcher
    opening webpage, email, or SMS from the app
ElevatedButton
	onPrimary: text, icons, overlay color
	primary: background fill
	onSurface: **disabled** text, icon, fill color
OutlinedButton
	primary: text, icons, overlay, pressed colors, 
	onSurface: **disabled** text, icon color
    feedback: backgroundColor

## packages


animation: prebuilt animations

flutter_svg
	use svg in flutter


[todo] testing
  [todo] mockito: mocking & verify matcher
  [todo] flutter_test: widget test
  [todo] flutter_driver: integration test
    [lazy] network_image_mock: ^1.0.2

[done] architecture
  model-viewModel-view
    mode: data
    viewModel: prepare data for presentation
    view: show things

[done] Dependency Injection
  [done] get_it: service locator to provide object implmentation (as an alternative to provider & inherited widget)


state management
  [done] provider: context-like state management
  [todo] event_bus: pub/subscribe pattern for decoupling application

navigation
  [done] url_launcher
  [todo] uni_links: deep link support

Authentication
  [todo] flutter_appauth: connect with OAuth and OpenID connect

network
  http: http request
  [todo] dio: wrapper over http
    interceptors
  [lazy] connectivity: get network status
  [lazy] flutter_offline: handle offline
  [lazy] system_proxy: easier to grab network request

local storage
  [done] shared_preferences
  [done] flutter_secure_storage (encryted)
  [lazy] hive (encrypted)

utils
  json_annotation: JSON serialization/deserialization
  json_serializable: generate class to convert class to JSON
  flutter_launcher_icons: simplify updating app's launcher icons
  flutter_native_splash: simplify updating app's splash screen
  package_info: query version code
  [todo] intl: internationalization
    [todo] localize message
	[todo] date & number formatting
  [lazy] clock: wrapper for clock api
  [lazy] string_unescape: ?
  [lazy] fake_async: test util for async functions
  [lazy] email_validator: validate email
    

[lazy]assets
  cupertino_icons: ^0.1.3
  [lazy] google_fonts: ^1.1.0: load font by http

[lazy]analytics
  [lazy] flutter_segment: ^3.0.0
    [lazy] firebase_analytics：google analytics for apps

[lazy]ci/cd
  [lazy] environment_config: ^2.2.3

[lazy] config
  [lazy] flutter_launcher_icons
  [lazy] flutter_launcher_name

[lazy] UI widgets
  [lazy] dots_indicator: dot-based progress bar
  [lazy] month_picker_dialog: md style date picker
	[lazy] loading_overlay: overlay for loading indicators
	[lazy] slider_button: just a button
  [lazy] pin_code_text_field: enter a password
  [lazy] webview_flutter: 
  [lazy] bot_toast: custom toast
  [lazy] dotted_border: add dotted border around widget
  [lazy] flutter_svg: draw svg on widget
  [lazy] infinite_scroll_pagination: infinite scroll
  [lazy] auto_size_text: auto resize text to fit within bounds
  [lazy] shimmer: skeleton screen effects
  [lazy] CachedNetworkImage: automatic cache network image
  [lazy] infinite_scroll_pagination
	PagingController
		holding state
		request new page


[lazy] Notifications
  [lazy] notification_permissions: check notification permission

[lazy] Hardware
  [lazy] detect phone shake

lint
    pedantic: a set of lint rules used by Google

Service integration
	[lazy] firebase_core
  [done] build_runner: dart code generator

  deep linking
    deferred link
    firebase dynamic link: https://firebase.google.com/docs/dynamic-links
  firebase_messaging
  auth0


## error handling
- FlutterError.onError


## themeing
ThemeData
	Color Theme
		PrimarySwatch
	Text Theme
	Theme for individual Widget



mock nav service

placeholder
visiblility detect placeholder


each isolate have its own memory and event loop

types of xss
    reflected
    stored

https://xss-game.appspot.com/


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

## error handling
- runZoneGuarded
    - create an error zone that wraps the app

- isolate.current.addErrorListener: 
	- any errors that may occur within the entry function

- FlutterError.onError
	- layout exceptions (e.g. overflow)
	- anything uncaught during widget build



## The good
- stateful hot reload

## The Bad
- no storybook to showcase design
- widget test done through several pumps
- pumpAndSettle somes doesn't work
	when there is background animation
- Cupertino Switch color cannot be controlled through themes
- popup is a route
- loading image assets
	- can not load nested directories
	- no svg support
- Tab is hardcoding the height
intellij editor Flutter inspector cannot connect
	disable devtools in the flutter section of the editor


## The Ugly


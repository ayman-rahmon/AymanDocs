# Views & View Groups


* ViewGroup is a container.
* frame layout is typically used to block out one area on the screen to display one view .
* Grid layout : views fil out cells in a grid with the ability of one view filling multiple cells.
* constraints layout allows you to place views Relativily to the parent View and other views and it also allows you to use constraints to determines how views should be positioned and scaled relative to the other views {complicated layouts without nested layouts}.

## the states of a view:
1. visible: visible for the user and it fills it's place.
2. invisible: not visible for the user but it still fills it's place.
3. gone : not visible for the user and it doesn't fill it's place.


## data binding:
the data binding library is a support library that allows you to bind UI components in your layouts to data sources in your app using a declarative format rather than programmatically.


### steps to use data binding:
1. enable data binding in gradle.
2. add <layout > as the root tag to the UI.
3. create a binding instance.
4. set the content view using databinding util.
5. bind each attribute in the views to the corresponding data.

#### in xml
```
<TextView
android:text="@{viewmodel.userName}"/>

```
#### in java
```
TextView view = findViewById(R.id.sample_text) ;
view.setText(viewModel.getUserName());

```


## Accessibility:

### examples:
1. talkback : to interact with your device using touch and spoken feedback.
2. explore by touch.
3. Accessibility settings.

* enable focus based navigation.






## Fragments:

* fragments are reusable pieces of UI.
* charactiristics of fragments:
	* have own life cycle.
	* can attach and detach while Activity is running.
	* can be used in multiple Activities.
	* flexible UI


### Fragment Lifecycle:
* directly affected by host life cycle.
* Fragment lifecycle control methods:
	* onCreatView
	* onDestroyView
	* onStart
	* onPause
	* onStopped
	* onResume
* programatically managing attaching and detaching fragments in android happens using a FragmentManager.

```
FragmenManager  m = getSupportFragmentManager();
// use the following line to attach fragments to fragment containers...(which are defined in xml).
m.beginTransaction().add(container,  Fragment);
```

* FragmentManager lets you add , remove or replace fragmets at runtime.
* to dynamically change fragments, you'll need a container view to reference their location and hold each fragment.
* static fragments (that don't change during run time ) don not need a container or transactions. instead they can just just be given the be specified in the xml file.

```

<androidx.fragment.app.FragmentContainerView
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/fragment_container_view"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:name="com.example.ExampleFragment" />

```

# intents


## what are they ?
intents are messaging objects that can be used to request an action from another app component.like one of the following:
* starting an activity.
* starting a service (service is a background process).
* delivering a broadcast (broadcast is a message that any app can receive).



## intent types:

intents come in one of two types :
* Explicit intents : specifiy which application will satisfy the intent , by supplying either the target app's package name or a fully-qualified component class name . typically this type of intent is used to start a component in your own app.
* implicit intents : do not name a specific component, but instead declare a general action to perform, which allows other apps to access this action. E.g: if you want your app to be able to show a location on the map , you can use an implicit intent to request that another capable app show a specified location on the map.


in the implicit intents usually we use a predefined urls for multiple activities,
E.g: geo url (which are used to display or convay a location on a map...) that has the main form of :
```
map URI:geo:{longitude},{Altitude}
```
The general form of the urls is :
```
//
scheme:[//user:password@host[:port]][/]path[?query][#fragment]

```
you can use uri builder to build the url in code like the following :
```
// building the uri ...
Uri.Builder builder = new Uri.Builder();

builder.Scheme("geo").path("0,0").query(address String);
Uri address = builder.build();

// adding the uri and the info to an intent...
Intent intent = new  Intent(Intent.ActionView);
intent.setData(address);
```

## share data using explicit Inents:

you can use explicit intent and put data in them to be sent with the intent itself, E.g:
```
// first parameter (current context) , second parameter (the context of the Activity we want to start)...
Intent intent = new Intent(this, SecondActivity.class) ;
// key is a String value that will be used to Access the date in the second Activity... while data is the actual data you want to send in one of the primitive data type (or a custome data type that is parcelable )
intent.putExtra(key , data) ;


startActivity(intent);
```
on the second Activity we can check for extras in the method onCreate and get them if existed like the following:
```
// getIntent() ==> gets the intent that started this Activity...
Intent intent = getIntent() ;
// hasExtras() ==> returns true if the Intent has Extras(data) sent with it ...
if(intent.hasExtras()) {
// you can get the data you want here using the appropriate methods and keys like...
// default being a default value if the data wasn't found...
intent.getStringExtra(key,default); // the default values in these methods are optional since there are overloaded methods of each of these methods with just the key in them as a parameter.
intent.getParcelableExtra(key , default);
intent.getIntExtra(key,default);
// or you can use the following in the newer versions of android...
intent.getExtras().getString(key);// you can also add a default value in this method
}
```






### share compat:

an Extra helper fucntionality for sharing data between activities.

```
ShareCompat.IntentBuilder.form(this)
.setChooserTitle(title:String)
.setType(MIMETYPE) // MIME type (Strin media type)
.setText(text); // text : String...
```
###MIME (multiple Intent mail Extension )
media type String, examples :
* text/plain
* text/rtf
* image/png
* video/mp4
the general format is :
{top-level-type-name}/{subtype name}


## intent filters:
intent filters are added to app components in the projectś manifest, and it accepts and action and a category or maybe some meta data sometimes(if needed)
* action : declares the intent action accepter, in name attribute. The value must be a literal string value of an action, not the class constant.
* data: declares the type of data accepted , using one or more attributes that specify various aspects of the data URI (scheme , host, port , path) and MIME type.
* category : declares the intent category accepted, in the name attribute. the value must be the literal string value of an action, not the class constant.

usually we define some intent filters to activities to enable them to used by the implicit intents also (for the activity to be able to be used implicitly it need to have an intent filter in itś manifest decliration)

### examples of manifest declared activities with intent filters
```
<activity android:name="MainActivity">
<!-- this activity is the main activity and the main entry point of the app so u need to specify it as such using an intent filter -->
<intent-filter>
	<action android:name="android.intent.actionṂAIN"/>
	<category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
</activity>

<activity android:name="ShareActivity">
<!-- this activity handles "SEND" actions with text data -->
<intent-filter>
	<action android:name="android.intent.actionṢEND"/>
	<category android:name="android.intent.category.DEFAULT"/>
	<data android:mimeType="text/plain"/>
</intent-filter>

    <!-- This activity also handles "SEND" and "SEND_MULTIPLE" with media data -->
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
        <action android:name="android.intent.action.SEND_MULTIPLE"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:mimeType="application/vnd.google.panorama360+jpg"/>
        <data android:mimeType="image/*"/>
        <data android:mimeType="video/*"/>
    </intent-filter>

</activity>
```

* ACTION_MAIN : indicates that this is the main entry point and doesn't expect any intent data.
* CATEGORY_LAUNCHER : indicates that this activity's icon should be placed in the system's app launcher . (if the activity doesn't specify an icon then the icon of the application will be used instead).


The second activity, ShareActivity, is intended to facilitate sharing text and media content. Although users might enter this activity by navigating to it from MainActivity, they can also enter ShareActivity directly from another app that issues an implicit intent matching one of the two intent filters.

### custom implicit intent example:

[example](https://stackoverflow.com/a/25747414/6562660)



### intent matching:

intents are mached against intent filters not only to discover a target component to activate, but also to discover something about the set of components on the device .



to call or resolve all the possible intents registered on the device you can use the following code:
```
// the acion name can be one from the prefined actions or a custom action that you created...
Intent sendIntent = new Intent(Intent.ACTION_SNED);
// this says something like "share this photo with"
String title = getResources().getString(R.string.chooser_title);
// create intent to show the chooser dialog...
Intent chooser = Intent.createChooser(sendIntent,title);
// verify the original intent will resolve to at least one detected activity...
if(sendIntentṛesolveActivity(getPackageManager())!= null){
// start the chosen activity from the chooser dialog...(this can be used to share data , posts , content vids , or anything)
startActivity(chooser);
}
```

if you want to use implicit intents to do some of the common things they're used for without creating your custome action you can check the page for common intents(these are used by developers to look for applications with activities that can handle the actions in the list):

[commonIntents](https://developer.android.com/guide/components/intents-common)

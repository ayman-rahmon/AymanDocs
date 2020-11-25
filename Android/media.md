# Media


## audio apps:



[audio apps](../images/MediaAudioApps.png)


```
MediaPlayer player = MediaPlayer.create(context , uri , display) ;
player.start () ;



// after done with the sound
player.release() ;

```

 [player logic](../images/playerLogic.png)



 ## video apps:


 * in video apps media sessions are completely tied to the UI.


 [video apps](../images/VideoApp.png)



 * wither for video or for media apps MediaPlayer supports little customizations and thats why we use something like ExoPlayer.

### ExoPlayer:


[ExoPlayer](../images/ExoPlayer.png)



#### custom player:

[custome ExoPlayer](../images/CustomPlayer.png)


* ExoPlayer support most of the formats and has high customizability.
* the following things are customizable :
  1. Renderer.
  2. Extractor.
  3. Media Source.
  4. track selector.
  5. LandControl.
  6. DataSource.

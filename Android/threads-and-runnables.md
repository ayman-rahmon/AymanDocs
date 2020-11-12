# Threads And Runnables




thread declaration :


```
Thread thread = new Thread(new Runnable(){

@override
public void run(){
// database logic there...
// and/or background processes...
}

}).start();

```

thread declaration with updating the ui on the main ui thread :


```
Thread thread = new Thread(new Runnable(){

public void run(){
// backgroun process

runOnUiThread(new Runnable(){
// run some stuff on the main ui thread like updating the the ui (process bar and )
});

}

}).start();

```

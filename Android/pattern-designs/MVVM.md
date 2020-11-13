# MVVM patter design


![MVVM network](../images/MVVM-structure-network.png)







![MVVM paged list](../images/MVVM-structure.png)




* The movie repository contains two data sources, Network , and database.
* The Repository merges the content of the data sources via MediatorLiveData , in order to avoid duplicate content,  we defined DIFF_CALLBACK in the model.





## coding example:

![coding example](https://github.com/ayman-rahmon/MovieApp)

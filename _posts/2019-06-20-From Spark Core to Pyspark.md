Apache spark is a fast execution engine that can run standalone or on yarn. The architectural foundation of spark lies on Resilient Distributed Dataset (RDDs). RDDs are read only data items that are split to be processes across multiple machines. It is the heart of Spark Core. 

Spark Core is the foundation of the overall project. It provides distributed task dispatching, scheduling, and basic I/O functionalities, exposed through an application programming interface (for Java,Python,Scala and R) centered on the RDD abstraction. The RDD API is simpler than programming in Map Reduce Hadoop framework, still it needs considerable programming experience. 

To ease the development, Spark SQL provides SQL like syntax. It is an abstraction over the RDDs and provides dataframes like R and python Pandas. It comes with Domain Specific language (DSL) to manipulate dataframes in Scala,Java or Python. The Dataset API provides more compile time checks. It is available in Java and Scala. The Dataset API is not available for python, as it is an interpreted language.

Spark Streaming uses Spark Core's fast scheduling capability to perform streaming analytics. Spark MLLIB is the spwcialized machine learning API that is built to take advantage of the horsepower of the cluster.




 

In my work, I have been using Spark/Scala mainly for ETL process. I am excited to figure out other ways to use spark. My journey hit a snag as I hit access issues with the site dsw.optum.com. Nilay mentioned that we can use spark on local as well. As I already had spark 2.4 on my local, I figured I can try that. The world of open source welcomed me with open arms.

First came the versioning issues. Spark by default comes with Python 2.7. So does anaconda2, the app that is available on secure. I had to get Paython3 separately. For anaconda I had to create a separate environment and set it to use Python3. I had to use conda -n “environment-name” to install the packages.

The spark instructions were much more conflicting. There are multiple ways to do it. The simplest way was the one that matched the instructions within pyspark.sh (within spark installation). I had to set up the PYTHON_DRIVER as jupyter and PYTHON_DRIVER_OPS as notebook. My excitement knew no bounds as I typed in pyspark in my shell. Instead of browser opening I found ‘notebook’ cannot be found.  Executing jupyter-notebook or ‘jupyter notebook’ after activating the right conda environment. I was hitting a big wall.
Another way to connect jupyter to pyspark was using findspark package. Following the instructions did not get the right python version. After flipping back and forth between various approaches, I did conda install of pyspark and findspark to my python3 conda environment. A few corrections to the python/spark paths and I tried jupyter notebook on the command line. Import findpark worked, import pyspark……..said a few prayers and finally success. At least I can use some of pyspark functionality to start.

It does not open from within jupyterlab but at least I do a wordcount on spark. 




[https://stackoverflow.com/questions/42371257/cant-launch-pyspark-in-browser-windows-10](https://stackoverflow.com/questions/42371257/cant-launch-pyspark-in-browser-windows-10)
[https://towardsdatascience.com/getting-started-with-python-environments-using-conda-32e9f2779307](https://towardsdatascience.com/getting-started-with-python-environments-using-conda-32e9f2779307)
[https://stackoverflow.com/questions/33814005/how-to-import-pyspark-in-anaconda](https://stackoverflow.com/questions/33814005/how-to-import-pyspark-in-anaconda)
[https://stackoverflow.com/questions/38411914/the-spark-home-env-variable-is-set-but-jupyter-notebook-doesnt-see-it-windows](https://stackoverflow.com/questions/38411914/the-spark-home-env-variable-is-set-but-jupyter-notebook-doesnt-see-it-windows)

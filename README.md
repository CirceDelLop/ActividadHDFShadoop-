# Actividad HDFS hadoop

## 1. Inicializar el cluster\n
```
cd hadoop
sudo ./start-container.sh
```
Salida

![Salida esperada.](https://i.imgur.com/K4adQE0.png)

- Iniciar con 2 esclavos y un maestro
- Entraremos al contenedor master

## 2. Iniciar hadoop
```
./start-hadoop.sh
```
Salida

![Salida esperada.](https://i.imgur.com/67xH5Ph.png)

## 3. Un archivo txt de un libro

```
wget https://www.gutenberg.org/cache/epub/28885/pg28885.txt
```
Salida

![Salida esperada.](https://i.imgur.com/w53sh1C.png)

## 4. Crear un directorio
```
mkdir input
```

## 5. Crear un archivo tipo tar.gz
```
tar -czvf input/alicia.tar.gz pg28885.txt
```

-c: Generar archivo -z: Comprimir con gzip. -v: Progreso del proceso. -f: Especificar nombre del archivo.

## 6. Revisar los tamaños de nuestros archivos
```
ls -flarts input
```
Salida

![Salida esperada.](https://i.imgur.com/vtE9rGB.png)

## 7. Crear y mover directorio input al DFS de HADOOP
```
hdfs dfs -mkdir -p test
hdfs dfs -put input
```

## 8. Revisar nuestro input directorio en HADOOP
```
hdfs dfs –ls  input
```
Salida

![Salida esperada.](https://i.imgur.com/6ciNvR6.png)

## 9. Leer las primeras lineas de nuestro archivo en HADOOP
```
hdfs dfs -cat  input/alicia.tar.gz | zcat | tail -n 20
```
Salida

![Salida esperada.](https://i.imgur.com/f9oJDYy.png)

## 10. Eliminar el archivo en HADOOP
```
hdfs dfs –rm –f /user/rawdata/example/alicia.tar.gz
```

## 11. Ejecutar un trabajo en HADOOP
```
hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/sources/hadoop-mapreduce-examples-2.7.2-sources.jar org.apache.hadoop.examples.WordCount input output
```
Salida

![Salida esperada.](https://i.imgur.com/ND1l2BV.png)

## 12. Ver el resultado del trabajo en HADOOP
```
hdfs dfs -cat output/part-r-00000
```
Salida

![Salida esperada.](https://i.imgur.com/UOghGwu.png)

## Herramientas de deteccion.

Correr el siguiente comando para ver todos los archivos que han sifo modificados durante los últimos 2 dias.

```
find /home/yoursite/ -mtime -2 -ls
```

Modificando el parametro -mtime se puede cambiar la cantidad de dias durante los cuales se hayan producido modificaciones. por ejemplo los últimos 10 días:

```
find /home/yoursite/ -mtime -10 -ls
```

Otra herramienta util es `grep`. En este caso para buscar los archivos con referencia base64 (comunmente utilizado por los hackers) se puede utilizar el comando:

```
grep -ril base64 *
```

Esto lista los nombre de archivos. Se puede omitilar la `l` para ver el contenido del archivo deon el string base64 ocurre:

```
grep -ri base64 *
```
Tener en cuenta que "base64" puede ocurrir en codigo que es legítimo. CUIDADO ANTES DE BORRAR!!!

Una busqueda mas refinada podría ser algo como:

```
grep --include=*.php -rn /home/yoursite/ -e "base64_decode"
```

Este comando buscar en todos losarchivos de extension .php que incluyan el texto “base64_decode” e imprimira los resultados encontrados incluyendo el número de línea para poder encontrar fácilmente la ocurrencia en el archivo.

Si se detectan cadenas en común, también puede extenderse labusqueda usando el comando:

```
grep -irl "cadena-comun" *
```




### Carpeta de uploads.

El siguiente comando busca todos los archivos de la carpeta uploads que nos son archivos de imagenes y los escribe en un archivo con el nombre  `uploads-non-binary.log` 

```
find public_html/wp-content/uploads/ -type f -not -name "*.jpg" -not -name "*.png" -not -name "*.gif" -not -name "*.jpeg" -not -name “*.webp” >uploads-non-binary.log
```

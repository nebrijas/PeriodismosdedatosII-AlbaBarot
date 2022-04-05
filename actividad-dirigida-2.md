# Actividad dirigida 2

En esta parte de la Actividad Dirigida 2 ponemos el código en bruto para entender bien lo que hemos hecho en la otra actividad.  

# Librerías
El primer paso es importar la librería requests. Este paso nos permitirá bajarnos la página web en la que vamos a hacer el scrapping. La librería BeautifulSoup sirve para analizar los datos que nos hemos descargado en el paso previo. 

# Variables
El segundo paso es definir las variables. Lo primero es poner la URL de donde queremos sacar los datos ("https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/"). No solo sirve con poner la URL, debemos hacer la petición con req = requests.get(URL). 

Damos la instrucción de que si el estatus code es distinto:  if (req.status_code != 200) no puede hacer web sraping. Si req.status_code == 200, el código imprimirá "Vamos a por ello".

Para poder leer el contenido HTML de la web, pasamos el objeto a un objeto BeautifulSoup html = BeautifulSoup(req.text, "html.parser").

# Datos
Nuestras variables son países, oros, platas, bronces y totales. Debemos identificar todas las variables con la función find_all() para que las busque en la página web elegida y las seleccione. 

Vamos a repetir las instrucciones un total de 20 veces: for i in range (20), es decir, un bucle. El código imprimirá los números, con %d, y el texto con %s Gracias a el bucle va corriendo.

# Pregunta 
Hacemos la pregunta "¿QUIERES CONOCER LOS 20 PAÍSES QUE HAN OBTENIDO MÁS MEDALLAS EN 2020?". En el caso de que la persona pulse la tecla s, entonces significará que sí, el código imprime "De acuerdo".


```


from bs4 import BeautifulSoup
import requests
#Datos sobre los Juegos Olímpicos en 2020



respuesta=input('¿QUIERES CONOCER LOS 20 PAÍSES QUE HAN OBTENIDO MÁS MEDALLAS EN 2020?\n \n Si tu respuesta es Sí, presiona "s" \n')
if(respuesta == 's'):
  print('\nRESULTADOS DE LOS DATOS DE LOS JUEGOS OLÍMPICOS 2020\n')
  print ('PAÍSES')
  URL = "https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/"
  # Realizamos la petición a la web
  req = requests.get(URL)
  # Si el estatus code no es 200 no se puede leer la página
  if (req.status_code != 200):
    raise Exception("No se puede hacer Web Scraping en"+ URL)
  # Pasamos el contenido HTML de la web a un objeto BeautifulSoup()
  html = BeautifulSoup(req.text, "html.parser")
  # Obtenemos todos los divs donde están las entradas
  paises = html.find_all("th",{"class":"pais"})
  oros = html.find_all("td",{"class":"m_oro"})
  platas = html.find_all("td",{"class":"m_plata"})
  bronces = html.find_all("td",{"class":"m_bronce"})
  totales = html.find_all("td",{"class":"m_total"})
  for i in range (20):
    # Con el método "getText()" no nos devuelve el HTML
    print("%d. %s \nOro: %s Plata: %s Bronce: %s \n Total: %s \n " % (i+1, paises[i+1].text.strip(),oros[i].text.strip(),platas[i].text.strip(),bronces[i].text.strip(), totales[i].text.strip()))

else:
  print('Qué lástima, y...')
```

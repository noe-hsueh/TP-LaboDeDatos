# Notas del TP - Labo de Datos 

## Qué falta hacer 

1. Limpiar inconsistencia en nombres de Provincias, Ciudades, etc. 

   Tucumán vs SM de Tuc. etc. 

2. Ídem con provincias





**Recomendaciones**

- [ ] Cómo cambió el territorio de las aerolineas

- [ ] Gráfico de mapa, con puntos donde tamaño es cant de vuelos 

- [ ] Ir de lo macro a micro 

- [ ] Me paro en Buenos Aires, veo las aerolíneas más grandes

  Eso aplica para todos las otras provincias ? 

- [ ] Cuantificar el aumento de las aerolíneas 

- [ ]  Ver si la var Flybondi/Norw. predice mejor el aumento de vuelos Aerolíneas, Austral





````

Algo interactivo para hacer con leaflet ?? 
```{r}
leaflet() %>% 
  addTiles() %>% 
  addCircleMarkers(lng = v_2015$lon_origen, lat=v_2015$lat_origen)
```
````









**Código viejos**

````R
datos <- data.frame()
for (i in 2014:2020) {
  nombre_archivo <- paste('dataset/aterrizajes-y-despegues-registrados-por-eana-',
                          as.character(i), ".csv", sep="")
  datos_i <- read.csv(nombre_archivo, fileEncoding = 'latin1' , header = T, sep = ";", strip.white = T)
  datos   <- rbind(datos, datos_i)
}
datos$formato_fecha <- as.Date(datos$Fecha, format="%d/%m/%Y")

# Nos quedamos solo con los vuelos que parten de ARG y llegan a ARG
# datos_dom 
#   
# View(datos_2021 %>% drop_na(dist_rec_km) %>% 
#   filter(Tipo.de.Movimiento=="Despegue", dist_rec_km > 0, 
#          Clase.de.Vuelo..todos.los.vuelos. == "Regular", Pasajeros>0) %>% 
#   group_by(dist_rec_km, Fecha) %>% filter(row_number(Fecha)==1) )
# 
# 
# 
# datos_despegue_2 <-  datos_dom %>% 
#   filter(Tipo.de.Movimiento=="Despegue") %>% 
#   group_by(dist_rec_km)
# 
# datos_aterrizaje_2 <-  datos_dom %>% 
#   filter(Tipo.de.Movimiento=="Aterrizaje") %>% 
#   group_by(dist_rec_km)
# 
# datos_aterrizaje <-  datos_dom %>% 
#   filter(Fecha=="2021-01-01", Tipo.de.Movimiento=="Aterrizaje", Aeronave=="EMB-ERJ190100IGW", dist_rec_km==298)
# datos_despegue <-  datos_dom %>% 
#   filter(Fecha=="2021-01-01", Tipo.de.Movimiento=="Despegue", Aeronave=="EMB-ERJ190100IGW", dist_rec_km==298)
# 
# View(datos_dom[-1,] %>% 
#   # filter(Tipo.de.Movimiento=="Aterrizaje") %>% 
#   # filter(dist_rec_km > 0) %>% 
#   # arrange(Fecha, desc(dist_rec_km), desc(Pasajeros))
#   group_by(Tipo.de.Movimiento, Aeronave, dist_rec_km)
#   
#   )
# A continuar el finde 



```{r}
#Wikipedia
pag_wiki         <- read_html("https://en.wikipedia.org/wiki/List_of_airports_in_Argentina")
elemento_tabla   <-  html_element(pag_wiki, ".wikitable")
tabla_aeropuerto <- html_table(elemento_tabla) 
tabla_aeropuerto$Coordinates <- tabla_aeropuerto$Coordinates %>%strsplit("/") %>% sapply("[",2)
info_aeropuerto <-tabla_aeropuerto %>% 
  select(`City served`, Province, IATA, Coordinates) %>%
  rename(Salida_ANA = IATA) %>% 
  mutate(Llegada_ANA = Salida_ANA)
```


````







## Consultas 







### Segunda parte: Análisis exploratorio 

### Introducción

- Trabajaremos con los datos del 2019 y 2015
  - Por las low cost 
  - Por el cambio del gobierno
- Hipótesis: intuimos que hubo un cambio. 

**Filtros a aplicar al dataset**

- Nos quedamos solo con los vuelos regulares 
- Nos quedamos con los vuelos nacionales, pues nos interesa saber si con el boom de las low cost hubo más vuelos adentro del país, esp. a zonas menos conectadas. 

> Tienen que mostrarnos que pueden describir y explorar los datos, buscar patrones y relaciones entre variables, generar preguntas y representar los datos de forma eficiente para generar hipótesis que den posibles respuestas a las preguntas que plantearon. 



### Preguntas a contestar

<u>Parte descriptiva</u>

- Frecuencia de aerolíneas Antes vs Despues
  - Disgregar vuelos por "clase de aerolineas"
    - Low cost vs vuelos convencionales

- [ ]  Gráfico x estacionalidad 


- [ ]  Gráfico de freq x aeropuerto (provincias/ciudad)
- [ ]  Market share de aerolíneas 
- [ ]  Mapa de vuelos 

- ¿Cómo son los vuelos interciudades ?
  2. Las ciudades con más vuelos. 
  3. Y, ¿ cuáles son las menos conectadas del país ?
- **¿ Hubo algún cambio en los vuelos a zonas menos conectadas entre esos años?**
  - ¿Qué aerolíneas volaban hacia esas zonas ?
  - ¿Las low cost tienen vuelos a esos lugares ?
- ¿Qué tan menos conectadas son con respectos a las más conectadas? 



<u>Visualizaciones</u>

**Introducción**

Gráficos básicos con variables simples

- Barplot de freq



Gráficos más complejos

- Grafo de los vuelos 



### Conclusiones

- 



### Bonus track 



#### Insparaciones 

- https://www.mit.edu/~amidi/teaching/data-science-tools/tutorial/data-visualization-with-r/
- https://ici.radio-canada.ca/info/2021/05/frontieres-voyages-aeroports-quarantaine-tests-deplacements-regions-avions-covid-19/en
- 
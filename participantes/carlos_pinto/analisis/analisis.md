## Análisis

Para analizar la forma en la que se está movilizando la gente usando el servicio público, utilicé los datos de Recaudo Bogotá.

Debido al tamaño de este dataset, encontré que lo más recomendable era utilizar el paquete `data.table` de `R` para poder hacer parsing de estos datos de manera fácil y rápida.

Posteriormente, pude encontrar que existían algunas inconsistencias con las fechas, por lo que realicé un limpiado de los datos utilizando el siguiente script de `R`.

```R
library(data.table)
library(ggplot2)

# Read data from file (it may take a few minutes, depending on your computer)
mydata <- fread("Data Validaciones Desnormalizadas.txt")

# Performing some data cleaning due to different date formats
mydata[CLEARING_TEXTO == "01-03-2020", CLEARING_TEXTO := "01/03/2020"]
mydata[CLEARING_TEXTO == "02-03-2020", CLEARING_TEXTO := "02/03/2020"]
mydata[CLEARING_TEXTO == "03-03-2020", CLEARING_TEXTO := "03/03/2020"]
mydata[CLEARING_TEXTO == "04-03-2020", CLEARING_TEXTO := "04/03/2020"]
mydata[CLEARING_TEXTO == "05-03-2020", CLEARING_TEXTO := "05/03/2020"]
mydata[CLEARING_TEXTO == "06-03-2020", CLEARING_TEXTO := "06/03/2020"]
mydata[CLEARING_TEXTO == "07-03-2020", CLEARING_TEXTO := "07/03/2020"]
mydata[CLEARING_TEXTO == "08-03-2020", CLEARING_TEXTO := "08/03/2020"]
mydata[CLEARING_TEXTO == "09-03-2020", CLEARING_TEXTO := "09/03/2020"]
mydata[CLEARING_TEXTO == "10-03-2020", CLEARING_TEXTO := "10/03/2020"]
mydata[CLEARING_TEXTO == "11-03-2020", CLEARING_TEXTO := "11/03/2020"]
mydata[CLEARING_TEXTO == "12-03-2020", CLEARING_TEXTO := "12/03/2020"]
mydata[CLEARING_TEXTO == "13-03-2020", CLEARING_TEXTO := "13/03/2020"]
mydata[CLEARING_TEXTO == "14-03-2020", CLEARING_TEXTO := "14/03/2020"]
mydata[CLEARING_TEXTO == "15-03-2020", CLEARING_TEXTO := "15/03/2020"]
mydata[CLEARING_TEXTO == "16-03-2020", CLEARING_TEXTO := "16/03/2020"]
mydata[CLEARING_TEXTO == "17-03-2020", CLEARING_TEXTO := "17/03/2020"]
mydata[CLEARING_TEXTO == "18-03-2020", CLEARING_TEXTO := "18/03/2020"]

# Format dates
mydata[, FECHA := as.POSIXct(CLEARING_TEXTO, format = "%d/%m/%Y")]
```

# Análisis
Dada mi corta experiencia con R, decidí hacer un subset de los datos y analizaros en una herramienta que conocía mejor: Tableau Public. A continuación encontrarán algunos de los insights que encontré de estos datos:

## Estaciones con mayor tráfico en Marzo 2020
![alt text](/participantes/carlos_pinto/visualizacion/box_plot.png "Estaciones con mayor tráfico en Marzo 2020")

Como se puede apreciar en la gráfica, las estaciones con mayor tráfico son:
1. Cabecera Autopista Norte
2. Portal Américas
3. Cabecera Calle 80
4. Portal Suba
5. Portal Sur
6. Portal El Dorado
7. Cabecera Usme
8. San Mateo
9. Portal Tunal
10. Banderas P. Central

## Evolución uso de estación Autopista Norte
![alt text](/participantes/carlos_pinto/visualizacion/autonorte_line_plot_over_time.png "Evolución uso de estación Autopista Norte en Marzo 2020")

Al analizar la evolución del tráfico en la estación más utilizada, es posible ver cómo la tendencia de uso disminuye hacia el 18 de Marzo, cuando la mayoría de personas que no debe transportarse decide quedarse en casa. Este es el momento en el que podemos ver que el transporte comienza a ser utilizado por la población que realmente lo necesita.
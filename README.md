<img src="https://raw.githubusercontent.com/rentwais/app/main/static/logo.png" alt="logo" style="background-color:white; width:240px"> 


<br>


# RentwAIs

## Your AI rental helper



### Proyecto para Saturday's AI Madrid - Junio 2023


<br>

---

## Introducción

El objetivo inicial del proyecto: detectar fraudes en alquileres de pisos en portales inmobiliarios.

La limitación de los datos disponibles hizo modificar el enfoque del proyecto y predecir una estimación del precio de la propiedad para poder comparar, ya que no se dispone de datos no sesgados que prueben los anuncios que realmente son fraude.

Se ha desarrollado un modelo de aprendizaje automático para predecir los precios de propiedades en Madrid capital usando RandomForestRegressor.

__Este repositorio contiene el modelo entrenado en python para calcular estimaciones de precio. Si busca la app para usar el modelo, está en el repositorio [/rentwais/app](https://github.com/rentwais/app).__

---

## Pasos realizados

1. Se cargan con pandas los datos del CSV <code>'inmuebles.csv'</code> a un DataFrame.
2. Se eliminan las columnas que no aportan datos como created_at, updated_at, titulo, id...
3. Se codifican con <code>sklearn.preprocessing.**OneHotEncoder**</code> las variables categóricas: 
    
    * distrito
    * tipovivienda
    * calefaccion
    * localidad


4. Del dataframe resultante se seleccionan solo las caracteristicas numéricas y se elimina la variable objetivo <code>precio</code>.
5. Se entrenan todos los modelos de la lista de modelos, se comparan los resultados y se guarda en <code>best_model</code> el modelo que mejores resultados haya obtenido.

    <pre>
    modelos = [
        RandomForestRegressor(),
        GradientBoostingRegressor(),
        PLSRegression(),
        XGBRegressor(),
        DecisionTreeRegressor(),
    ]</pre>

6. El modelo con mejores resultados (en este caso <code>RandomForestRegressor</code>) se exporta a un archivo <code>rfModel.pckl</code> para ser importado en la aplicación de consulta.

---

## Visualizaciones

El notebook de Jupyter contiene visualizaciones de los datos así como de los resultados del modelo catalogados como 'chollos' distribuidos por distritos.


En el notebook hay además un ejemplo de otra manera de probar varios modelos y quedarse con el que mejor resultados obtiene, usando la libreria <code>sklearn.model_selection.**GridSearchCV**</code> para testear varios modelos ajustando ciertos parámetros. 

<code>best_estimator_</code> devuelve cual es el mejor modelo de los testeados, que en este caso coincide con el mismo del otro método y con puntuaciones similares ( <code>RandomForestRegressor</code> ).



```python
import pandas as pd
import numpy as np
import missingno as msno
%matplotlib inline
```


```python
#https://datos.gob.mx/busca/dataset/plan-de-apertura-institucional-de-hggea-de-hggea
path = 'plan_institucional.csv'
df = pd.read_csv(path, encoding='latin', error_bad_lines=False)
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Responsable</th>
      <th>Nombre del conjunto</th>
      <th>Nombre del recurso</th>
      <th>Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th>Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th>Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th>Frecuencia con la que actualizan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Administrador Institucional de Datos</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-08-28</td>
      <td>irregular</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Administrador Institucional de Datos</td>
      <td>Plan de Apertura Institucional de HGGEA de HGG...</td>
      <td>Plan de Apertura Institucional de HGGEA de HGG...</td>
      <td>Plan de Apertura Institucional de HGGEA</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>csv</td>
      <td>2015-09-25</td>
      <td>irregular</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Administrador Institucional de Datos</td>
      <td>Cursos impartidos en el Hospital de HGGEA</td>
      <td>Tabla con el nÃºmero de asistentes por cursos ...</td>
      <td>Tabla de los cursos impartidos en el Hospital,...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2019-02-27</td>
      <td>anual</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Administrador Institucional de Datos</td>
      <td>Causas de mortalidad hospitalaria de HGGEA</td>
      <td>Tabla de las causas registradas de mortalidad ...</td>
      <td>Tabla de las causas de mortalidad hospitalaria...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Administrador Institucional de Datos</td>
      <td>Residencias MÃ©dicas por especialidad de HGGEA</td>
      <td>Tabla con nÃºmero de Residentes por Especialidad</td>
      <td>Tabla con nÃºmero de Residentes por Especialid...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2019-03-15</td>
      <td>anual</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.info()

```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 14 entries, 0 to 13
    Data columns (total 9 columns):
    Responsable                                                           14 non-null object
    Nombre del conjunto                                                   14 non-null object
    Nombre del recurso                                                    14 non-null object
    Â¿De quÃ© es?                                                         14 non-null object
    Â¿Tiene datos privados?                                               14 non-null object
    RazÃ³n por la cual los datos son privados                             0 non-null float64
    Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?    13 non-null object
    Fecha estimada de publicaciÃ³n en datos.gob.mx                        14 non-null object
    Frecuencia con la que actualizan                                      14 non-null object
    dtypes: float64(1), object(8)
    memory usage: 1.1+ KB



```python
df.shape

```




    (14, 9)




```python
df.shape[0]

```




    14




```python
df.shape[1]

```




    9




```python
df.columns.values.tolist()

```




    ['Responsable',
     'Nombre del conjunto',
     'Nombre del recurso',
     'Â¿De quÃ© es?',
     'Â¿Tiene datos privados?',
     'RazÃ³n por la cual los datos son privados',
     'Â¿En quÃ© plataforma, tecnologÃ\xada, programa o sistema se albergan?',
     'Fecha estimada de publicaciÃ³n en datos.gob.mx',
     'Frecuencia con la que actualizan']




```python
df.dtypes

```




    Responsable                                                            object
    Nombre del conjunto                                                    object
    Nombre del recurso                                                     object
    Â¿De quÃ© es?                                                          object
    Â¿Tiene datos privados?                                                object
    RazÃ³n por la cual los datos son privados                             float64
    Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?     object
    Fecha estimada de publicaciÃ³n en datos.gob.mx                         object
    Frecuencia con la que actualizan                                       object
    dtype: object




```python
df.isnull().any().any()

```




    True




```python
msno.matrix(df)

```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f076c4221d0>




![png](output_9_1.png)



```python
df.replace({' ': np.nan}, inplace=True)

```


```python
df.isnull().any().any()

```




    True




```python
msno.matrix(df)

```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f076c341128>




![png](output_12_1.png)



```python
msno.bar(df)

```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f076c2c1c88>




![png](output_13_1.png)



```python
df.columns[df.isnull().any()].tolist()

```




    ['RazÃ³n por la cual los datos son privados',
     'Â¿En quÃ© plataforma, tecnologÃ\xada, programa o sistema se albergan?']




```python
df.describe()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>RazÃ³n por la cual los datos son privados</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>std</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>min</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>max</th>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.loc[[0]]

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Responsable</th>
      <th>Nombre del conjunto</th>
      <th>Nombre del recurso</th>
      <th>Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th>Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th>Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th>Frecuencia con la que actualizan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Administrador Institucional de Datos</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-08-28</td>
      <td>irregular</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.loc[30:33]

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Responsable</th>
      <th>Nombre del conjunto</th>
      <th>Nombre del recurso</th>
      <th>Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th>Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th>Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th>Frecuencia con la que actualizan</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
df.drop([0,4,8], axis=0).head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Responsable</th>
      <th>Nombre del conjunto</th>
      <th>Nombre del recurso</th>
      <th>Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th>Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th>Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th>Frecuencia con la que actualizan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Administrador Institucional de Datos</td>
      <td>Plan de Apertura Institucional de HGGEA de HGG...</td>
      <td>Plan de Apertura Institucional de HGGEA de HGG...</td>
      <td>Plan de Apertura Institucional de HGGEA</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>csv</td>
      <td>2015-09-25</td>
      <td>irregular</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Administrador Institucional de Datos</td>
      <td>Cursos impartidos en el Hospital de HGGEA</td>
      <td>Tabla con el nÃºmero de asistentes por cursos ...</td>
      <td>Tabla de los cursos impartidos en el Hospital,...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2019-02-27</td>
      <td>anual</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Administrador Institucional de Datos</td>
      <td>Causas de mortalidad hospitalaria de HGGEA</td>
      <td>Tabla de las causas registradas de mortalidad ...</td>
      <td>Tabla de las causas de mortalidad hospitalaria...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Administrador Institucional de Datos</td>
      <td>Protocolos por LÃ­neas de InvestigaciÃ³n en el...</td>
      <td>Tabla de Protocolos de investigaciÃ³n realizad...</td>
      <td>Tabla del total de Protocolos de investigaciÃ³...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2019-02-27</td>
      <td>anual</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Administrador Institucional de Datos</td>
      <td>Medicamentos y productos farmacÃ©uticos adquir...</td>
      <td>Tabla de medicamentos y productos farmacÃ©utic...</td>
      <td>Tabla de medicamentos y productos farmacÃ©utic...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>csv</td>
      <td>2019-07-31</td>
      <td>anual</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.drop(df.index[1:5], axis=0).head(10)

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Responsable</th>
      <th>Nombre del conjunto</th>
      <th>Nombre del recurso</th>
      <th>Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th>Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th>Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th>Frecuencia con la que actualizan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Administrador Institucional de Datos</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-08-28</td>
      <td>irregular</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Administrador Institucional de Datos</td>
      <td>Protocolos por LÃ­neas de InvestigaciÃ³n en el...</td>
      <td>Tabla de Protocolos de investigaciÃ³n realizad...</td>
      <td>Tabla del total de Protocolos de investigaciÃ³...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2019-02-27</td>
      <td>anual</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Administrador Institucional de Datos</td>
      <td>Medicamentos y productos farmacÃ©uticos adquir...</td>
      <td>Tabla de medicamentos y productos farmacÃ©utic...</td>
      <td>Tabla de medicamentos y productos farmacÃ©utic...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>csv</td>
      <td>2019-07-31</td>
      <td>anual</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Administrador Institucional de Datos</td>
      <td>Causas de morbilidad Hospitalaria  en el HGGEA</td>
      <td>Tabla de las causas de morbilidad Hospitalaria...</td>
      <td>Tabla de las causas de morbilidad hospitalaria...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Administrador Institucional de Datos</td>
      <td>Encuestas de satisfacciÃ³n de los usuarios del...</td>
      <td>Tabla de resultados de la encuesta de satisfac...</td>
      <td>Resultados de la encuesta de satisfacciÃ³n de ...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>Excel</td>
      <td>2019-10-31</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Administrador Institucional de Datos</td>
      <td>Pacientes atendidos en Consulta Externa segÃºn...</td>
      <td>Tabla de procedencia de los pacientes que son ...</td>
      <td>Total de pacientes atendidos en Consulta Exter...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Administrador Institucional de Datos</td>
      <td>Pacientes por grupo de edad y gÃ©nero de HGGEA</td>
      <td>Tabla de la distribuciÃ³n de pacientes que son...</td>
      <td>Tabla de la distribuciÃ³n de pacientes que son...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Administrador Institucional de Datos</td>
      <td>CirugÃ­as efectuadas en el Hospital</td>
      <td>Tabla de las cirugÃ­as efectuadas en el Hospital</td>
      <td>Tabla de las cirugÃ­as efectuadas en el Hospit...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Administrador Institucional de Datos</td>
      <td>Pacientes atendidos en Consulta Externa por ti...</td>
      <td>Tabla de pacientes atendidos en Consulta Exter...</td>
      <td>Tabla de pacientes atendidos en consulta exter...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Administrador Institucional de Datos</td>
      <td>Publicaciones del Ã¡rea de InvestigaciÃ³n del ...</td>
      <td>Tabla de Publicaciones del Ã¡rea de Investigac...</td>
      <td>Tabla de Publicaciones del Ã¡rea de Investigac...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-02-19</td>
      <td>anual</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[10:].head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Responsable</th>
      <th>Nombre del conjunto</th>
      <th>Nombre del recurso</th>
      <th>Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th>Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th>Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th>Frecuencia con la que actualizan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>Administrador Institucional de Datos</td>
      <td>Pacientes por grupo de edad y gÃ©nero de HGGEA</td>
      <td>Tabla de la distribuciÃ³n de pacientes que son...</td>
      <td>Tabla de la distribuciÃ³n de pacientes que son...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Administrador Institucional de Datos</td>
      <td>CirugÃ­as efectuadas en el Hospital</td>
      <td>Tabla de las cirugÃ­as efectuadas en el Hospital</td>
      <td>Tabla de las cirugÃ­as efectuadas en el Hospit...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Administrador Institucional de Datos</td>
      <td>Pacientes atendidos en Consulta Externa por ti...</td>
      <td>Tabla de pacientes atendidos en Consulta Exter...</td>
      <td>Tabla de pacientes atendidos en consulta exter...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Administrador Institucional de Datos</td>
      <td>Publicaciones del Ã¡rea de InvestigaciÃ³n del ...</td>
      <td>Tabla de Publicaciones del Ã¡rea de Investigac...</td>
      <td>Tabla de Publicaciones del Ã¡rea de Investigac...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-02-19</td>
      <td>anual</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.Responsable.values

```




    array(['Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos'], dtype=object)




```python
df['Responsable'].values

```




    array(['Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos',
           'Administrador Institucional de Datos'], dtype=object)




```python
df.Responsable.unique()

```




    array(['Administrador Institucional de Datos'], dtype=object)




```python
df.Responsable.value_counts()

```




    Administrador Institucional de Datos    14
    Name: Responsable, dtype: int64




```python
df.agg(['count', 'size', 'nunique'])

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Responsable</th>
      <th>Nombre del conjunto</th>
      <th>Nombre del recurso</th>
      <th>Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th>Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th>Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th>Frecuencia con la que actualizan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>0</td>
      <td>13</td>
      <td>14</td>
      <td>14</td>
    </tr>
    <tr>
      <th>size</th>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
    </tr>
    <tr>
      <th>nunique</th>
      <td>1</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>8</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('Responsable').agg(['count', 'size', 'nunique']).stack()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Nombre del conjunto</th>
      <th>Nombre del recurso</th>
      <th>Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th>Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th>Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th>Frecuencia con la que actualizan</th>
    </tr>
    <tr>
      <th>Responsable</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">Administrador Institucional de Datos</th>
      <th>count</th>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>0</td>
      <td>13</td>
      <td>14</td>
      <td>14</td>
    </tr>
    <tr>
      <th>size</th>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
    </tr>
    <tr>
      <th>nunique</th>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>8</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('Responsable').agg(['count', 'size', 'nunique'])

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">Nombre del conjunto</th>
      <th colspan="3" halign="left">Nombre del recurso</th>
      <th colspan="3" halign="left">Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>...</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th colspan="3" halign="left">Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th colspan="3" halign="left">Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th colspan="3" halign="left">Frecuencia con la que actualizan</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>size</th>
      <th>nunique</th>
      <th>count</th>
      <th>size</th>
      <th>nunique</th>
      <th>count</th>
      <th>size</th>
      <th>nunique</th>
      <th>count</th>
      <th>...</th>
      <th>nunique</th>
      <th>count</th>
      <th>size</th>
      <th>nunique</th>
      <th>count</th>
      <th>size</th>
      <th>nunique</th>
      <th>count</th>
      <th>size</th>
      <th>nunique</th>
    </tr>
    <tr>
      <th>Responsable</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Administrador Institucional de Datos</th>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>...</td>
      <td>0</td>
      <td>13</td>
      <td>14</td>
      <td>3</td>
      <td>14</td>
      <td>14</td>
      <td>8</td>
      <td>14</td>
      <td>14</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 24 columns</p>
</div>




```python
df_sample = df.sample(frac=0.05, random_state=1)
df_sample.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Responsable</th>
      <th>Nombre del conjunto</th>
      <th>Nombre del recurso</th>
      <th>Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th>Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th>Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th>Frecuencia con la que actualizan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Administrador Institucional de Datos</td>
      <td>Causas de mortalidad hospitalaria de HGGEA</td>
      <td>Tabla de las causas registradas de mortalidad ...</td>
      <td>Tabla de las causas de mortalidad hospitalaria...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.shape

```




    (14, 9)




```python
df_sample.shape

```




    (1, 9)




```python
df_dropped = df.dropna(subset=['Nombre del recurso'])
df_dropped.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Responsable</th>
      <th>Nombre del conjunto</th>
      <th>Nombre del recurso</th>
      <th>Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th>Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th>Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th>Frecuencia con la que actualizan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Administrador Institucional de Datos</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-08-28</td>
      <td>irregular</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Administrador Institucional de Datos</td>
      <td>Plan de Apertura Institucional de HGGEA de HGG...</td>
      <td>Plan de Apertura Institucional de HGGEA de HGG...</td>
      <td>Plan de Apertura Institucional de HGGEA</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>csv</td>
      <td>2015-09-25</td>
      <td>irregular</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Administrador Institucional de Datos</td>
      <td>Cursos impartidos en el Hospital de HGGEA</td>
      <td>Tabla con el nÃºmero de asistentes por cursos ...</td>
      <td>Tabla de los cursos impartidos en el Hospital,...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2019-02-27</td>
      <td>anual</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Administrador Institucional de Datos</td>
      <td>Causas de mortalidad hospitalaria de HGGEA</td>
      <td>Tabla de las causas registradas de mortalidad ...</td>
      <td>Tabla de las causas de mortalidad hospitalaria...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Administrador Institucional de Datos</td>
      <td>Residencias MÃ©dicas por especialidad de HGGEA</td>
      <td>Tabla con nÃºmero de Residentes por Especialidad</td>
      <td>Tabla con nÃºmero de Residentes por Especialid...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2019-03-15</td>
      <td>anual</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_dropped.shape

```




    (14, 9)




```python
df_copy = df.copy()
df_copy.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Responsable</th>
      <th>Nombre del conjunto</th>
      <th>Nombre del recurso</th>
      <th>Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th>Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th>Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th>Frecuencia con la que actualizan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Administrador Institucional de Datos</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-08-28</td>
      <td>irregular</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Administrador Institucional de Datos</td>
      <td>Plan de Apertura Institucional de HGGEA de HGG...</td>
      <td>Plan de Apertura Institucional de HGGEA de HGG...</td>
      <td>Plan de Apertura Institucional de HGGEA</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>csv</td>
      <td>2015-09-25</td>
      <td>irregular</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Administrador Institucional de Datos</td>
      <td>Cursos impartidos en el Hospital de HGGEA</td>
      <td>Tabla con el nÃºmero de asistentes por cursos ...</td>
      <td>Tabla de los cursos impartidos en el Hospital,...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2019-02-27</td>
      <td>anual</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Administrador Institucional de Datos</td>
      <td>Causas de mortalidad hospitalaria de HGGEA</td>
      <td>Tabla de las causas registradas de mortalidad ...</td>
      <td>Tabla de las causas de mortalidad hospitalaria...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Administrador Institucional de Datos</td>
      <td>Residencias MÃ©dicas por especialidad de HGGEA</td>
      <td>Tabla con nÃºmero de Residentes por Especialidad</td>
      <td>Tabla con nÃºmero de Residentes por Especialid...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2019-03-15</td>
      <td>anual</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_copy.shape

```




    (14, 9)




```python
df_copy.agg(['count', 'size', 'nunique'])

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Responsable</th>
      <th>Nombre del conjunto</th>
      <th>Nombre del recurso</th>
      <th>Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th>Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th>Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th>Frecuencia con la que actualizan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>0</td>
      <td>13</td>
      <td>14</td>
      <td>14</td>
    </tr>
    <tr>
      <th>size</th>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
    </tr>
    <tr>
      <th>nunique</th>
      <td>1</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>8</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
list(df['Responsable'].unique())

```




    ['Administrador Institucional de Datos']




```python
keys = list(df['Responsable'].unique())
vals = range(1,8)
act = dict(zip(keys, vals))
act
```




    {'Administrador Institucional de Datos': 1}




```python
df_copy['Nombre del recurso'] = df['Responsable'].map(act)
df_copy.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Responsable</th>
      <th>Nombre del conjunto</th>
      <th>Nombre del recurso</th>
      <th>Â¿De quÃ© es?</th>
      <th>Â¿Tiene datos privados?</th>
      <th>RazÃ³n por la cual los datos son privados</th>
      <th>Â¿En quÃ© plataforma, tecnologÃ­a, programa o sistema se albergan?</th>
      <th>Fecha estimada de publicaciÃ³n en datos.gob.mx</th>
      <th>Frecuencia con la que actualizan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Administrador Institucional de Datos</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>1</td>
      <td>Inventario Institucional de Datos de HGGEA</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-08-28</td>
      <td>irregular</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Administrador Institucional de Datos</td>
      <td>Plan de Apertura Institucional de HGGEA de HGG...</td>
      <td>1</td>
      <td>Plan de Apertura Institucional de HGGEA</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>csv</td>
      <td>2015-09-25</td>
      <td>irregular</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Administrador Institucional de Datos</td>
      <td>Cursos impartidos en el Hospital de HGGEA</td>
      <td>1</td>
      <td>Tabla de los cursos impartidos en el Hospital,...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2019-02-27</td>
      <td>anual</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Administrador Institucional de Datos</td>
      <td>Causas de mortalidad hospitalaria de HGGEA</td>
      <td>1</td>
      <td>Tabla de las causas de mortalidad hospitalaria...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2020-01-13</td>
      <td>trimestral</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Administrador Institucional de Datos</td>
      <td>Residencias MÃ©dicas por especialidad de HGGEA</td>
      <td>1</td>
      <td>Tabla con nÃºmero de Residentes por Especialid...</td>
      <td>Publico</td>
      <td>NaN</td>
      <td>application/vnd.ms-excel</td>
      <td>2019-03-15</td>
      <td>anual</td>
    </tr>
  </tbody>
</table>
</div>




```python
list(df_copy['Nombre del recurso'].unique())

```




    [1]



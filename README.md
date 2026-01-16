# Pokedex


## 📃 Descripción General
Este dashboard fue diseñado para revisar algunas estadísticas base e información del Pokemon (incluye Megaevoluciones).

<p align="center"><img width="411" height="273" alt="image" src="https://github.com/user-attachments/assets/75cdc45d-6a51-4818-8bf2-22fe329b0515" /></p>

## 📊 Contenido del proyecto
- Página de "Pokedex": Contiene una vista general por Pokemon y forma.


## 🛠️ Herramientas y Tecnologías Utilizadas
- Visualización: Power BI Desktop.
- Fuente de Datos:
  - [PokemonForms.csv (Tabla Principal)](https://github.com/Gbarrantes25/Pokedex-PowerBI/blob/main/Data%20Source/FactPokemon.csv)
  - [DimPokemon.csv](https://github.com/Gbarrantes25/Pokedex-PowerBI/blob/main/Data%20Source/DimPokemon.csv)
  - [DimEvolution.csv](https://github.com/Gbarrantes25/Pokedex-PowerBI/blob/main/Data%20Source/DimEvolution.csv)
  - [DimTypePokemon.csv](https://github.com/Gbarrantes25/Pokedex-PowerBI/blob/main/Data%20Source/DimTypePokemon.csv)
  - [DimRegion.csv](https://github.com/Gbarrantes25/Pokedex-PowerBI/blob/main/Data%20Source/DimRegion.csv)
  - [DimPokemonForm](https://github.com/Gbarrantes25/Pokedex-PowerBI/blob/main/Data%20Source/DimPokemonForm.csv)
 
    
- Lenguajes: DAX para las medidas calculadas y Power Query (Lenguaje M) para la transformación de datos.

## ⚙️ Configuración del Entorno
- Conexión a internet.
- Software Necesario: Power BI Desktop.
- Instalación:
  - Descargar [Pokedex v2.pbix](https://github.com/Gbarrantes25/Pokedex-PowerBI/raw/refs/heads/main/Pokedex%20v2.pbix) con Power BI Desktop.
  - Entrar a Inicio y darle click a "Actualizar".


## 📂 Estructura del Repositorio
<code>.
  ├── Data Source/                                              # Contiene los archivos fromato .csv
  |—— Mega-Evolution/                                           # Contiene imágenes de las megavoluciones.
  ├── Dashboard (box 3 degradado gris negro Pokemon v2).svg     # Es el archivo de fondo del lienzo del proyecto.
  ├── Pokedex v2.pbix                                           # Archivo que será ejecutado con Power BI Desktop.
  └── README.md                                                 # Este archivo.
</code>


## ✅ Características Principales
- Transformaciones en Power Query: Se realizaron procesos de limpieza y modelado de datos para optimizar el rendimiento.
- Medidas DAX: Se implementaron medidas para concatenaciones y validaciones.
  - <code>Ability = 
            VAR TextAbility = CONCATENATEX(DimAbilities,DimAbilities[Ability],", ")
            RETURN
              IF(ISBLANK(TextAbility),"",TextAbility)
    </code>
  - <code>Description = 
            VAR TextDescription = CONCATENATEX(DimCharacteristics,DimCharacteristics[Description])
            RETURN
              IF(ISBLANK(TextDescription),"",TextDescription)
    </code>
  - <code>Region = 
            VAR TextRegion = TOPN(1,VALUES(DimRegion[Nombre_Region]))
            RETURN 
              IF(ISBLANK(TextRegion),"",TextRegion)
    </code>
  - <code>Size(cm) = 
            VAR Valor = SUM(DimCharacteristics[Size])
            RETURN
              IF(OR(ISBLANK(Valor),Valor=0),0,Valor)
    </code>
  - <code>Weight(kg) = 
            VAR Valor = SUM(DimCharacteristics[Weight])
            RETURN
              IF(OR(ISBLANK(Valor),Valor=0),0,Valor)
    </code>
  
- Medidas DAX para crear Columnas Calculadas: Se implementaron medidas para crear columnas calculadas.
  - Tabla PokemonForms
    - <code>Url_ImgType = RELATED(DimTypePokemon[Url_ImgType])</code> (para traer la imagen de los tipos).
  - Tabla DimPokemon
    - <code>Search = DimPokemon[IdPokemon]&" - "&DimPokemon[Nombre_Pokemon]</code> (Columna pensada para buscar por número o nombre de pokemon).
  - Tabla DimEvolution
    - <code>IndexId = INT(TRIM(LEFT(DimEvolution[IdEvolution],2)))</code> (Columna para crear un índice de ordenamiento).
    - <code>Type1 = LOOKUPVALUE(DimTypePokemon[Type],DimTypePokemon[IdType],DimEvolution[IdType1])</code> (Columna para traer el tipo1 del Pokemon).
    - <code>Type2 = LOOKUPVALUE(DimTypePokemon[Type],DimTypePokemon[IdType],DimEvolution[IdType2])</code> (Columna para traer el tipo2 del Pokemon).

- Medidas DAX para crear tablas puente:
  - <code>IdForms = VALUES(PokemonForms[IdForm])</code>
  - <code>DimIdEvo = VALUES(DimEvolution[IdEvolution])</code>

- Modelado de datos:
  <details>
    <summary>Captura de modelado</summary>
      <img width="1757" height="943" alt="image" src="https://github.com/user-attachments/assets/da19a84e-88a7-4846-9e84-6da611bf5958" />
  </details>
  
- Diseño Interactivo: Uso de segmentación de datos.


## 🖼️ Vistas Previas del proyecto
<details>
  <summary>Capturas</summary>

  ![Animation2](https://github.com/user-attachments/assets/9eb48803-4d08-467a-b096-ec5befa93ece)


  ![Animation3](https://github.com/user-attachments/assets/20ed72ca-0917-4978-9796-440cf7599d74)


</details>


## 👤 Autor
- Giancarlo Barrantes
- Lima, Perú
- [Linkedin](https://www.linkedin.com/in/gb25/)

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
  - <code>_FilterSlicerForm = COUNT(FactPokemon[IdForm])</code>
  - <code>_FilterTableDetails = 
              VAR IsUniqueContext = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
              VAR EvolutionCount = DISTINCTCOUNT(FactPokemon[IdEvolution])
              RETURN IF(IsUniqueContext, EvolutionCount, 0)
    </code>
  - Calc
    - <code>_ATK = 
          VAR IsContextUnique = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
      	  VAR result = IF(IsContextUnique,AVERAGEX(FactPokemon,FactPokemon[Atk]),0)
      	  RETURN result
      </code>
    - <code>_DEF = 
          VAR IsContextUnique = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
      	  VAR result = IF(IsContextUnique,AVERAGEX(FactPokemon,FactPokemon[Def]),0)
      	  RETURN result
      </code>
    - <code>_HP = 
          VAR IsContextUnique = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
      	  VAR result = IF(IsContextUnique,AVERAGEX(FactPokemon,FactPokemon[Hp]),0)
      	  RETURN result
      </code>
    - <code>_SP ATK = 
          VAR IsContextUnique = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
      	  VAR result = IF(IsContextUnique,AVERAGEX(FactPokemon,FactPokemon[Sp Atk]),0)
      	  RETURN result
      </code>
    - <code>_SP DEF = 
          VAR IsContextUnique = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
      	  VAR result = IF(IsContextUnique,AVERAGEX(FactPokemon,FactPokemon[Sp Def]),0)
      	  RETURN result
      </code>
    - <code>_SPD = 
          VAR IsContextUnique = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
      	  VAR result = IF(IsContextUnique,AVERAGEX(FactPokemon,FactPokemon[Spd]),0)
      	  RETURN result
      </code>
    - <code>_TOTALSTATS = 
          VAR IsContextUnique = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
	        VAR total = AVERAGEX(FactPokemon,[_HP] + [_ATK] + [_DEF] + [_SP ATK] + [_SP DEF] + [_SPD])
	        VAR result = IF(IsContextUnique,total,0)
	        RETURN result
      </code>
    - <code>_SIZE = 
          VAR IsContextUnique = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
	        VAR result = IF(IsContextUnique,AVERAGEX(FactPokemon,Related(DimPokemonForm[Size (cm)])),"?")
	        RETURN result
      </code>
    - <code>_WEIGHT =
          VAR IsContextUnique = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
	        VAR result = IF(IsContextUnique,AVERAGEX(FactPokemon,Related(DimPokemonForm[Weight (kg)])),"?")
	        RETURN result
      </code>
  - Images
    - <code>_ImgPokemonMain = 
          VAR IsContextUnique = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
          VAR img = "https://images.wikidexcdn.net/mwuploads/wikidex/6/6a/latest/20230115164405/Pok%C3%A9_Ball_EP.png"
          VAR UrlImgPokemon = MAXX(FactPokemon,RELATED(DimPokemonForm[Url_ImgPokemonForm]))
          VAR result = IF(IsContextUnique,UrlImgPokemon,img)
          RETURN result
      </code>
    - <code>_ImgType1 = 
          VAR IsContextUnique = HASONEVALUE ( DimPokemon[IdSearch] ) && HASONEVALUE ( DimPokemonForm[FormPokemon] )
          VAR ImgTransparent = "https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Images/transparent.png"
          VAR UrlImgType = MAXX ( FactPokemon, RELATED ( DimTypePokemon[Url_IgType] ) )
          VAR result = IF ( IsContextUnique, UrlImgType, ImgTransparent )
          RETURN result
      </code>
    - <code>_ImgType2 = 
          VAR IsContextUnique = HASONEVALUE ( DimPokemon[IdSearch] ) && HASONEVALUE ( DimPokemonForm[FormPokemon] )
          VAR ImgTransparent = "https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Images/transparent.png"
          VAR UrlType2 = CALCULATE (SELECTEDVALUE ( DimTypePokemon[Url_IgType] ),USERELATIONSHIP ( FactPokemon[IdType2], DimTypePokemon[IdType] ),CROSSFILTER ( FactPokemon[IdType2], DimTypePokemon[IdType], BOTH ))
          VAR result = SWITCH (TRUE (),IsContextUnique && NOT ( ISBLANK ( UrlType2 ) ), UrlType2,IsContextUnique && ( ISBLANK ( UrlType2 ) ), ImgTransparent,NOT ( IsContextUnique ), ImgTransparent)
        RETURN result
      </code>
    - <code>_ImgEvolution = 
          VAR Context1 = HASONEVALUE ( DimPokemon[IdSearch] ) && HASONEVALUE ( DimPokemonForm[FormPokemon] )
          VAR Context2 = HASONEVALUE ( DimPokemon[IdSearch] ) && HASONEVALUE ( DimPokemonForm[FormPokemon] ) && HASONEVALUE ( DimEvolution[IdEvolution] )
          VAR ImgEmpty = "https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Images/selectvalueslicer.png"
          VAR ImgNoEvolution = "https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Images/hasnoevolution.png"
          VAR UrlImg = MAXX ( TOPN(1,FactPokemon,FactPokemon[IdEvolution],ASC), RELATED ( DimEvolution[Url_ImgEvolution] ) )
          VAR result = SWITCH (TRUE (),Context1, IF ( ISBLANK ( UrlImg ), ImgNoEvolution, UrlImg ),Context2, IF ( ISBLANK ( UrlImg ), ImgNoEvolution, UrlImg ),NOT ( Context1 ), ImgEmpty)
          RETURN result
      </code>
    - <code>_ImgkeyStoneMain = 
          VAR IsContextUnique = HASONEVALUE ( DimPokemon[IdSearch] ) && HASONEVALUE ( DimPokemonForm[FormPokemon] )
          VAR ImgTransparent = "https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Images/transparent.png"
          VAR MegaKeyStone = "https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Mega-Evolution/Piedra_activadora_serie_Pok%C3%A9mon.png"
          VAR FormPokemon = MAXX ( FactPokemon, RELATED(DimPokemonForm[FormPokemon]) )
          VAR result =IF (IsContextUnique && CONTAINSSTRING ( FormPokemon, "- Mega" ),MegaKeyStone,ImgTransparent)
          RETURN result
      </code>
    - <code>_ImgKeyStoneEvolution = 
          VAR IsContextUnique = HASONEVALUE ( DimPokemon[IdSearch] ) && HASONEVALUE ( DimPokemonForm[FormPokemon] )
          VAR ImgTransparent = "https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Images/transparent.png"
          VAR MegaKeyStone = "https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Mega-Evolution/Piedra_activadora_serie_Pok%C3%A9mon.png"
          VAR Evolution = MAXX ( FactPokemon, RELATED ( DimEvolution[NameEvo] ) )
          VAR result = SWITCH (TRUE (),IsContextUnique && ISBLANK ( Evolution ), ImgTransparent,IsContextUnique && CONTAINSSTRING ( Evolution, "Mega-" ), MegaKeyStone,IsContextUnique && NOT ( CONTAINSSTRING ( Evolution, "Mega-" ) ), ImgTransparent,NOT ( IsContextUnique ), ImgTransparent)
          RETURN result
      </code>
  - Visual Interactivity
    - <code>_abilitiestext = 
          VAR IsContextUnique = HASONEVALUE(DimPokemonForm[FormPokemon]) && HASONEVALUE(DimPokemon[IdSearch])
          VAR RegionValue = MAXX(FactPokemon,RELATED(DimPokemonForm[Ability]))
          RETURN IF(IsContextUnique, RegionValue, "?")
      </code>
    - <code>_backgroundcolorregion = 
	        VAR kantobackground = "#FDE7ED"
        	VAR johtobackground = "#FDF6B9"
        	VAR hoennbackground = "#DAFDBA"
        	VAR sinnohbackground = "#E6F3FF"
        	VAR unovabackground = "#F2F2F2"
        	VAR kalosbackground = "#FCBAE3"
        	VAR alolabackground = "#FFC8B8"
        	VAR galarbackground = "#EBD7FC"
        	VAR hisuibackground = "#EBDECC"
        	VAR paldeabackground = "#BFC2F8"
        	VAR nobackground = "#ffffff00"
	        VAR result =SWITCH(TRUE(),
          		[_regiontext] = "Kanto", kantobackground,
          		[_regiontext] = "Johto", johtobackground,
          		[_regiontext] = "Hoenn", hoennbackground,
          		[_regiontext] = "Sinnoh", sinnohbackground,
          		[_regiontext] = "Unova", unovabackground,
          		[_regiontext] = "Kalos", kalosbackground,
          		[_regiontext] = "Alola", alolabackground,
          		[_regiontext] = "Galar", galarbackground,
          		[_regiontext] = "Hisui", hisuibackground,
          		[_regiontext] = "Paldea", paldeabackground,
		          ISBLANK([_regiontext]), nobackground)
	        RETURN result
      </code>
    - <code>_descriptiontext = 
          VAR IsContextUnique = HASONEVALUE(DimPokemonForm[FormPokemon]) && HASONEVALUE(DimPokemon[IdSearch])
          VAR DescriptionValue = MAXX(FactPokemon,RELATED(DimPokemonForm[Description]))
          RETURN IF(IsContextUnique, DescriptionValue, "?")
      </code>
    - <code>_evolutiontitle = 
          VAR IsContextUnique = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
          VAR NameEvo = MINX(FactPokemon, RELATED(DimEvolution[NameEvo]))
          RETURN IF(IsContextUnique && NOT(ISBLANK(NameEvo)) && LEFT(NameEvo,5)="Mega-","Mega Evolution","Evolution")
      </code>
    - <code>_regiontext = 
          VAR IsContextUnique = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
          VAR regionValue = MAXX(FactPokemon, RELATED(DimRegion[Region]))
          RETURN IF(IsContextUnique,regionValue,"?")
      </code>
    - <code>_statstitle = 
	        VAR IsContextUnique = HASONEVALUE(DimPokemon[IdSearch]) && HASONEVALUE(DimPokemonForm[FormPokemon])
          VAR result = "Stats base" & IF(IsContextUnique," (" & [_TOTALSTATS] & ")","")
	        RETURN result
      </code>
    - <code>_fontcolorregion = 
        	VAR kantocolorfont = "#ED124C"
        	VAR johtocolorfont = "#CC9300"
        	VAR hoenncolorfont = "#397204"
        	VAR sinnohcolorfont = "#0070D1"
        	VAR unovacolorfont = "#696969"
        	VAR kaloscolorfont = "#CA077C"
        	VAR alolacolorfont = "#FB4604"
        	VAR galarcolorfont = "#6D2FD0"
        	VAR hisuicolorfont = "#76582E"
        	VAR paldeacolorfont = "#141FBD"
        	VAR transparentfont = "#ffffff00"
          VAR result =SWITCH(TRUE(),
          		[_regiontext] = "Kanto", kantocolorfont,
          		[_regiontext] = "Johto", johtocolorfont,
          		[_regiontext] = "Hoenn", hoenncolorfont,
          		[_regiontext] = "Sinnoh",sinnohcolorfont,
          		[_regiontext] = "Unova", unovacolorfont,
          		[_regiontext] = "Kalos", kaloscolorfont,
          		[_regiontext] = "Alola", alolacolorfont,
          		[_regiontext] = "Galar", galarcolorfont,
          		[_regiontext] = "Hisui", hisuicolorfont,
          		[_regiontext] = "Paldea", paldeacolorfont,
          		ISBLANK([_regiontext]), transparentfont)
          return result
      </code>

- Modelado de datos:
  <details>
    <summary>Captura de modelado</summary>
      <img width="1554" height="939" alt="image" src="https://github.com/user-attachments/assets/641bebcd-a027-41d4-87a6-b29a92ff7dbd" />
  </details>
  
- Diseño Interactivo: Uso de segmentación de datos.


## 🖼️ Vistas Previas del proyecto
<details>
  <summary>Capturas</summary>

  ![Animation2](https://github.com/user-attachments/assets/9eb48803-4d08-467a-b096-ec5befa93ece)


  ![Animation3](https://github.com/user-attachments/assets/20ed72ca-0917-4978-9796-440cf7599d74)


  [![Título del gdfgVideo]([https://img.freepik.com/vector-premium/icono-video-png_564384-173.jpg](https://github.com/user-attachments/assets/75cdc45d-6a51-4818-8bf2-22fe329b0515))]([https://www.youtube.com/watch?v=VIDEO_ID](https://www.youtube.com/watch?v=z-FERNIn5QY))
  [![fdgdfgdfg](https://img.freepik.com/vector-premium/icono-video-png_564384-173.jpg)](https://www.youtube.com/watch?v=z-FERNIn5QY)

</details>


## 👤 Autor
- Giancarlo Barrantes
- Lima, Perú
- [Linkedin](https://www.linkedin.com/in/gb25/)

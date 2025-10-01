# Pokedex


## 📃 Descripción General
Este dashboard fue diseñado para revisar algunas estadísticas base e información del Pokemon (no incluye Megaevoluciones).

<p align="center"><img width="411" height="273" alt="image" src="https://github.com/user-attachments/assets/75cdc45d-6a51-4818-8bf2-22fe329b0515" /></p>

## 📊 Contenido del proyecto
- Página de "Pokedex": Contiene una vista general por Pokemon y forma.


## 🛠️ Herramientas y Tecnologías Utilizadas
- Visualización: Power BI Desktop.
- Fuente de Datos:
  - [PokemonForms.csv (Tabla Principal)](https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Fuente%20de%20Datos/PokemonForms.csv)
  - [DimPokemon.csv](https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Fuente%20de%20Datos/DimPokemon.csv)
  - [DimEvolution.csv](https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Fuente%20de%20Datos/DimEvolution.csv)
  - [DimCharacteristics.csv](https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Fuente%20de%20Datos/DimCharacteristics.csv)
  - [DimTypePokemon.csv](https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Fuente%20de%20Datos/DimTypePokemon.csv)
  - [DimAbilities.csv](https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Fuente%20de%20Datos/DimAbilities.csv)
  - [DimStats.csv](https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Fuente%20de%20Datos/DimStats.csv)
  - [DimRegion.csv](https://raw.githubusercontent.com/Gbarrantes25/Pokedex-PowerBI/refs/heads/main/Fuente%20de%20Datos/DimRegion.csv)
 
    
- Lenguajes: DAX para las medidas calculadas y Power Query (Lenguaje M) para la transformación de datos.


## ⚙️ Configuración del Entorno
- Software Necesario: Power BI Desktop.
- Instalación:
  - Descargar [Pokedex.pbix](https://github.com/Gbarrantes25/Pokedex-PowerBI/blob/main/Pokedex.pbix) con Power BI Desktop.
  - Entrar a Inicio y darle click a "Actualizar".


## 📂 Estructura del Repositorio
<code>.
  ├── Fuentes de Datos/                                         # Contiene los archivos de datos de ejemplo (.CSV)
  ├── Dashboard (box 3 degradado gris negro Pokemon v2).svg     # Es el archivo de fondo del lienzo del proyecto.
  ├── Pokedex.pbix                                              # Archivo que será ejecutado con Power BI Desktop.
  └── README.md                                                 # Este archivo.
</code>


## ✅ Características Principales
- Transformaciones en Power Query: Se realizaron procesos de limpieza y modelado de datos para optimizar el rendimiento.
- Medidas DAX: Se implementaron cálculos para los KPI's del Revenue Management.
  - <code>%Occ = DIVIDE([Total RNs],[RNs Disponibles],0)</code>
  - <code>Conteo Días = COUNT(Calendario[Date])</code>
  - <code>RNs Disponibles = SUMX(Habitaciones,Habitaciones[Cantidad de Habitaciones]*[Conteo Días])</code>
  - <code>ADR = DIVIDE([Total Revenue],[Total RNs],0)</code>
  - <code>Total Revenue = SUMX(Reservaciones,Reservaciones[RN]*Reservaciones[Precio Unitario])</code>
  - <code>Total RNs = SUM(Reservaciones[RN])</code>
  - <code>RevPar = [ADR]*[%Occ]</code>
  - <code>Total A&B = SUM(Reservaciones[A&B])</code>
- Medidas Formateadas DAX: Se implementaron medidas formateadas para visualizar de manera corta los números extensos ("B", "M" y "K").
  - <code>ADR*** = 
          VAR T = ABS([ADR])
          RETURN
              SWITCH(TRUE(),
                  T >= 1000000000, FORMAT(T, "$#,,,.00 B"),
                  T >= 1000000, FORMAT(T, "$#,,.00 M"),
                  T >= 1000, FORMAT(T, "$#,.00 K"),
                      SUBSTITUTE(FORMAT(T, "$#.00"),",","."))
    </code>
  - <code>RNs*** = 
          VAR T = [Total RNs]
          RETURN
              SWITCH(TRUE(),
                  T >= 1000000000, FORMAT(T, "#,,,.00 B"),
                  T >= 1000000, FORMAT(T, "#,,.00 M"),
                  T >= 1000, FORMAT(T, "#,.00 K"),
                      FORMAT(T,"0"))
    </code>
  - <code>Revenue*** = 
          VAR T = [Total Revenue]
          RETURN
              SWITCH(TRUE(),
                  T >= 1000000000, FORMAT(T, "$#,,,.00 B"),
                  T >= 1000000, FORMAT(T, "$#,,.00 M"),
                  T >= 1000, FORMAT(T, "$#,.00 K"),
                      FORMAT(T,"$0.00"))
    </code>
  - <code>A&B*** = 
          VAR T = [Total A&B]
          RETURN
              SWITCH(TRUE(),
                  T >= 1000000000, FORMAT(T, "$#,,,.00 B"),
                  T >= 1000000, FORMAT(T, "$#,,.00 M"),
                  T >= 1000, FORMAT(T, "$#,.00 K"),
                      FORMAT(T,"$0"))
    </code>
- Diseño Interactivo: Uso de paginado para navegación y segmentación de datos.


## 🖼️ Vistas Previas del proyecto
<details>
  <summary>Capturas</summary>


  Página "Regions"


  ![Animation1](https://github.com/user-attachments/assets/0d3de5f3-ae65-43e6-abc6-72e97e6a6be9)


  Página "Hotel Branches"


  ![Animation2](https://github.com/user-attachments/assets/0d347ecd-a7cb-496e-940e-a18ad0723a01)


</details>


## 👤 Autor
- Giancarlo Barrantes
- Lima, Perú
- [Linkedin](https://www.linkedin.com/in/gb25/)

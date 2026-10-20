# Elementos transponibles en *Fusarium*: Análisis *in silico*

Código y datos de partida de mi Trabajo de Fin de Grado en Bioquímica (Universidad de Sevilla, 2026), centrado en el estudio bioinformático de elementos transponibles (TEs) en el hongo *Fusarium*.

El análisis se realiza en un cuaderno de Jupyter (`Secuencias.ipynb`) y se complementa con alineamientos y árboles de *neighbor-joining* (NJ) hechos manualmente en MEGA.

## Cuaderno

1. **Familia Fot** (*F. oxysporum*): lee Fot1-Fot10, genera un multifasta y construye un árbol NJ a partir del alineamiento de ADN.
2. **ORFs y proteínas**: busca el ORF más largo de cada elemento transponible (ambas cadenas, 3 marcos), lo traduce y genera `proteinas_TE.fasta`. Con las proteínas Fot construye un segundo árbol.
3. **TEF1** (gen *housekeeping*): alinea el gen en 8 especies de *Fusarium* y dibuja su árbol NJ.
4. **Carotenoides**: concatena `carB + carO + carX` por especie, alinea y dibuja el árbol NJ.

Los alineamientos se hacen con MUSCLE y los árboles con Biopython (`DistanceCalculator('identity')` + `DistanceTreeConstructor().nj`). Las figuras se guardan en `images/`.

## Estructura del repositorio

```
.
├── Secuencias.ipynb        Cuaderno con el análisis
├── F.fujikuroi (pseudo-impala).fasta
├── F.vertici (pseudo-skippy).fasta
├── Fot/                    Secuencias Fot1-Fot10
├── Folyt1/ impala/ Skippy/ Drifter/ Hormin/ Tfo1/
│                           Secuencias de otras familias de TEs
├── housekeeping/           Secuencias del gen TEF1 por especie
├── Carotenoides/           Genes carB, carO y carX por especie
│   ├── carotenoides_alineamiento_MEGA.fas   Alineamiento hecho en MEGA
│   └── carotenoides_arbol_MEGA.mtsx         Árbol NJ (sesión de MEGA)
├── images/                 Árboles generados (PNG)
├── environment.yml         Entorno de Python
└── LICENSE
```

## Cómo reproducirlo

1. Clone el repositorio y cree el entorno:
   ```bash
   conda env create -f environment.yml
   conda activate tfg-fusarium
   ```
2. Descargue **MUSCLE v3.x** (el código usa la sintaxis `-in` / `-out`, que corresponde a la versión 3) desde la web ([drive5.com](https://drive5.com/muscle/)) y coloque el ejecutable en la raíz del proyecto como `muscle.exe` (Windows). En Linux o macOS, se debe cambiar el argumento `muscle` de la función `alinear_y_arbol` por la ruta del ejecutable.
3. Abra `Secuencias.ipynb` y ejecute *Kernel → Restart & Run All*.

El cuaderno regenera los multifastas, los alineamientos y las imágenes; por eso esos archivos intermedios no se incluyen en el repositorio (ver `.gitignore`).

## Análisis hechos con MEGA

Parte de los alineamientos y de los árboles NJ se hicieron manualmente con **MEGA 12** (interfaz gráfica), no desde el cuaderno. Parámetros:

- Alineamiento: *MUSCLE* (desde Python, ver cuaderno); importado a *MEGA* para el árbol.
- Modelo de distancia: *Maximum Composite Likelihood* (nucleótidos, transiciones + transversiones; tasas uniformes).
- Tratamiento de huecos: *pairwise deletion*.
- Bootstrap: no.

Nota importante: Los árboles del cuaderno usan distancia de identidad (proporción de diferencias) y los de MEGA el modelo indicado arriba, así que pueden no coincidir exactamente.

## Origen de las secuencias

Las secuencias proceden del NCBI. Los numeros de acceso se encuentran en la memoria del trabajo.

## Licencia

Código bajo licencia MIT (ver `LICENSE`).

## Autor

*[Alberto García Sosa]*· Realizado en el grado en Bioquímica por la Universidad de Sevilla y la de Málaga.

[cite_start]PROYECTO: Motor de búsqueda para plataformas de streaming [cite: 1]
[cite_start]CURSO: Programación III [cite: 2]

[cite_start]Enlace de repositorio de GitHub: https://github.com/ALexx-Carri/ProyectoProgaIII [cite: 3]

[cite_start]INTEGRANTES: [cite: 4]

| Nombre y apellido | Codigo |
| :--- | :--- |
| Alvaro Mallky Alagón Aguilar | 202520221 |
| Sebastian Falvy Mendoza | 202510469 |
| Omar Sotelo Cusi | 202510448 |
| Joaquim Alexander Carrión Diaz | 202510461 |
| Rodrigo Muñoz Dominguez | [cite_start]202410784 | [cite: 5]

[cite_start]Objetivo del proyecto: [cite: 6]
[cite_start]El proyecto tiene como objetivo desarrollar una plataforma de streaming capaz de administrar y realizar búsquedas eficientes de películas a partir de información almacenada en archivos CSV previamente limpiados. [cite: 7]
[cite_start]La plataforma permitirá realizar búsquedas por palabras exactas, frases y subcadenas parciales, con el propósito de optimizar la búsqueda de información dentro de títulos y sinopsis de películas. [cite: 8]
[cite_start]Para esta tarea, el sistema implementa tres estructuras de datos: [cite: 9]
[cite_start]Inverted Index: Es una estructura que almacena palabras completas y las relaciona con las películas en las que aparecen. [cite: 10]
[cite_start]Su función principal es permitir una búsquedas exactas de acceso rapido. [cite: 11]
[cite_start]Suffix Tree: Es un árbol que almacena todos los sufijos posibles de un texto. [cite: 12]
[cite_start]Esto permite realizar búsquedas parciales o por subcadenas dentro de palabras y frases. [cite: 13]
[cite_start]El sistema puede encontrar coincidencias incluso cuando el usuario busca solo una parte de la palabra. [cite: 14]
[cite_start]Búsqueda híbrida: Combinación entre algoritmos previamente mencionados, el Inverted Index se utiliza para localizar rápidamente películas candidatas mediante coincidencias exactas, mientras que el Suffix Trie permite verificar coincidencias parciales dentro de dichas películas sobrantes. [cite: 15]
[cite_start]Esta combinación reduce el tiempo de búsqueda en sistemas de grandes volúmenes de información. [cite: 16]

| Estructura | Tipo de búsqueda |
| :--- | :--- |
| inverted Index | búsqueda exacta por palabras |
| Suffix Trie | búsqueda parcial por subcadenas |
| [cite_start]Búsqueda Híbrida | búsqueda por frases y coincidencias complejas | [cite: 17]

[cite_start]Además se implementa un sistema de recomendación utilizando un enfoque de Content-Based Filtering , recomendando películas según similitudes en género, palabras clave, contenido de la sinopsis, e interacciones realizadas por el usuario mediante “Like”. [cite: 18]
[cite_start]Asimismo, para determinar la relevancia de una película al momento de la búsqueda, el sistema asigna un puntaje acumulativo basado en los criterios ya mencionados. [cite: 19]
[cite_start]Tecnologías Utilizadas [cite: 20]
[cite_start]IDE utilizado: CLion [cite: 21]
[cite_start]Lenguaje de programación: C++20 [cite: 22]
[cite_start]Control de versiones: Git y GitHub [cite: 23]
[cite_start]Librerías utilizadas: STL (Standard Template Library) [cite: 24]
[cite_start]Formato de almacenamiento de datos: CSV [cite: 25]

[cite_start]Arquitectura: [cite: 26]
[cite_start]El sistema sigue una arquitectura modular orientada al procesamiento, almacenamiento y búsqueda eficiente de información de películas. [cite: 27]
[cite_start]El flujo inicia con la lectura de archivos CSV que contienen títulos, sinopsis y atributos como género, director y elenco. [cite: 28]
[cite_start]Posteriormente, los datos pasan por una etapa de limpieza y tokenización, donde se normalizan caracteres, se eliminan símbolos innecesarios y el texto se divide en palabras para optimizar las búsquedas. [cite: 29]
[cite_start]Una vez procesados los datos, el sistema construye dos estructuras principales: un Inverted Index, encargado de relacionar palabras completas con las películas donde aparecen para realizar búsquedas exactas, y un Suffix Trie, utilizado para búsquedas parciales o por subcadenas dentro de títulos y sinopsis. [cite: 30]
[cite_start]Ambas estructuras son utilizadas por un motor de búsqueda híbrida que combina precisión y eficiencia. [cite: 31]
[cite_start]El Inverted Index permite filtrar rápidamente películas candidatas mediante coincidencias exactas, mientras que el Suffix Trie complementa el proceso verificando coincidencias parciales dentro de los resultados obtenidos. [cite: 32]
[cite_start]Finalmente, el sistema organiza las películas mediante un algoritmo de relevancia que prioriza coincidencias en títulos, sinopsis, tags e interacciones del usuario, mostrando como resultado las cinco películas más relevantes según la búsqueda realizada. [cite: 33]

[cite_start]Clases y estructuras del programa: [cite: 34]

[cite_start]Movie: La clase Movie representa la información principal de cada película almacenada dentro del sistema. [cite: 35]
[cite_start]Contiene atributos correspondientes a los datos obtenidos desde el archivo CSV. [cite: 36]

```cpp
class Movie {
private:
    int id;
    int releaseYear;

    string title;
    string originEthnicity;
    string director;

    vector<string> cast;
    vector<string> genres;

    string wikiPage;
    string plot;

public:
    int getId();
    string getTitle();
    string getPlot();
};

http://googleusercontent.com/immersive_entry_chip/0
http://googleusercontent.com/immersive_entry_chip/1
http://googleusercontent.com/immersive_entry_chip/2
http://googleusercontent.com/immersive_entry_chip/3
http://googleusercontent.com/immersive_entry_chip/4
http://googleusercontent.com/immersive_entry_chip/5
http://googleusercontent.com/immersive_entry_chip/6
http://googleusercontent.com/immersive_entry_chip/7
http://googleusercontent.com/immersive_entry_chip/8
http://googleusercontent.com/immersive_entry_chip/9
http://googleusercontent.com/immersive_entry_chip/10
http://googleusercontent.com/immersive_entry_chip/11
http://googleusercontent.com/immersive_entry_chip/12
http://googleusercontent.com/immersive_entry_chip/13
http://googleusercontent.com/immersive_entry_chip/14
http://googleusercontent.com/immersive_entry_chip/15
http://googleusercontent.com/immersive_entry_chip/16
http://googleusercontent.com/immersive_entry_chip/17
http://googleusercontent.com/immersive_entry_chip/18

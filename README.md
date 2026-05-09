¡Claro que sí! Aquí tienes todo el contenido estructurado en formato Markdown, ideal para copiar y pegar directamente en el archivo README.md de tu repositorio.He organizado las secciones, tablas y bloques de código para que se visualicen perfectamente en GitHub.PROYECTO: Motor de búsqueda para plataformas de streaming   CURSO: Programación III Repositorio: ProyectoProgaIII   👥 Integrantes   Nombre y apellidoCódigoAlvaro Mallky Alagón Aguilar   202520221   Sebastian Falvy Mendoza   202510469   Omar Sotelo Cusi   202510448   Joaquim Alexander Carrión Diaz   202510461   Rodrigo Muñoz Dominguez   202410784   🎯 Objetivo del proyecto   El proyecto tiene como objetivo desarrollar una plataforma de streaming capaz de administrar y realizar búsquedas eficientes de películas a partir de información almacenada en archivos CSV previamente limpiados. La plataforma permitirá realizar búsquedas por palabras exactas, frases y subcadenas parciales, con el propósito de optimizar la búsqueda de información dentro de títulos y sinopsis de películas.  Para esta tarea, el sistema implementa tres estructuras de datos/búsqueda:  Inverted Index: Es una estructura que almacena palabras completas y las relaciona con las películas en las que aparecen. Su función principal es permitir una búsquedas exactas de acceso rapido.  Suffix Tree (Trie): Es un árbol que almacena todos los sufijos posibles de un texto. Esto permite realizar búsquedas parciales o por subcadenas dentro de palabras y frases. El sistema puede encontrar coincidencias incluso cuando el usuario busca solo una parte de la palabra.  Búsqueda híbrida: Combinación entre algoritmos previamente mencionados, el Inverted Index se utiliza para localizar rápidamente películas candidatas mediante coincidencias exactas, mientras que el Suffix Trie permite verificar coincidencias parciales dentro de dichas películas sobrantes. Esta combinación reduce el tiempo de búsqueda en sistemas de grandes volúmenes de información.  Tipos de Búsqueda   EstructuraTipo de búsquedaInverted Index   búsqueda exacta por palabras   Suffix Trie   búsqueda parcial por subcadenas   Búsqueda Híbrida   búsqueda por frases y coincidencias complejas   ⭐ Sistemas AdicionalesSistema de Recomendación: Se implementa un sistema utilizando un enfoque de Content-Based Filtering, recomendando películas según similitudes en género, palabras clave, contenido de la sinopsis, e interacciones realizadas por el usuario mediante “Like”.  Sistema de Relevancia: Para determinar la relevancia de una película al momento de la búsqueda, el sistema asigna un puntaje acumulativo basado en los criterios ya mencionados.  🛠️ Tecnologías Utilizadas   IDE utilizado: CLion   Lenguaje de programación: C++20   Control de versiones: Git y GitHub   Librerías utilizadas: STL (Standard Template Library)   Formato de almacenamiento de datos: CSV   🏗️ Arquitectura   El sistema sigue una arquitectura modular orientada al procesamiento, almacenamiento y búsqueda eficiente de información de películas.  Entrada de Datos: El flujo inicia con la lectura de archivos CSV que contienen títulos, sinopsis y atributos como género, director y elenco.  Procesamiento: Posteriormente, los datos pasan por una etapa de limpieza y tokenización, donde se normalizan caracteres, se eliminan símbolos innecesarios y el texto se divide en palabras para optimizar las búsquedas.  Construcción de Árboles: Una vez procesados los datos, el sistema construye dos estructuras principales: un Inverted Index, encargado de relacionar palabras completas con las películas donde aparecen para realizar búsquedas exactas, y un Suffix Trie, utilizado para búsquedas parciales o por subcadenas dentro de títulos y sinopsis.  Búsqueda y Salida: Ambas estructuras son utilizadas por un motor de búsqueda híbrida que combina precisión y eficiencia. El Inverted Index permite filtrar rápidamente películas candidatas mediante coincidencias exactas, mientras que el Suffix Trie complementa el proceso verificando coincidencias parciales dentro de los resultados obtenidos. Finalmente, el sistema organiza las películas mediante un algoritmo de relevancia que prioriza coincidencias en títulos, sinopsis, tags e interacciones del usuario, mostrando como resultado las cinco películas más relevantes según la búsqueda realizada.  💻 Clases y estructuras del programa   Movie   La clase Movie representa la información principal de cada película almacenada dentro del sistema. Contiene atributos correspondientes a los datos obtenidos desde el archivo CSV.  C++class Movie {
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
(Código basado en la estructura definida para la clase Movie )  InvertedIndex   La clase InvertedIndex es responsable de almacenar la relación entre palabras y películas. Su función principal es permitir búsquedas exactas rápidas dentro de títulos y sinopsis.  C++class InvertedIndex {
    unordered_map<string, vector<int>> index;
};
(Código basado en la estructura definida para la clase InvertedIndex )  SuffixNode y SuffixTrie   La estructura SuffixNode representa un nodo dentro del Suffix Trie, donde cada nodo almacena un carácter y las conexiones hacia los siguientes caracteres posibles. La clase SuffixTrie administra la construcción y recorrido del Trie de sufijos para permitir búsquedas parciales y coincidencias internas.  C++struct SuffixNode {
    unordered_map<char, SuffixNode*> children;
    bool isEnd;
};

class SuffixTrie {
    SuffixNode* root;
};
(Código basado en la estructura definida para SuffixNode y SuffixTrie )  SearchEngine   Actúa como el motor principal de búsqueda del sistema. Se encarga de coordinar el uso del Inverted Index y el Suffix Trie para realizar búsquedas híbridas y devolver resultados relevantes al usuario.  C++class SearchEngine {
    InvertedIndex index;
    SuffixTrie trie;
};
(Código basado en la estructura definida para la clase SearchEngine )  CSVReader   Tiene como función leer y procesar los archivos CSV que contienen la información de las películas, y enviar los datos procesados hacia las estructuras de búsqueda.  C++class CSVReader {
    vector<Movie> movies;
};
(Código basado en la estructura definida para la clase CSVReader )  📝 Algoritmos y Pseudocódigos   A continuación, se detalla la lógica central del sistema:1. Limpieza de datos y Tokenización   Proceso para garantizar búsquedas consistentes (eliminación de duplicados, corrección de encoding) y división del texto en palabras.  PlaintextALGORITMO LimpiarDatos 
ENTRADA: archivoCSV
SALIDA: peliculasLimpias
INICIO
    Lectura del archivoCSV
    PARA CADA fila EN archivoCSV HACER
        Eliminar registros duplicados
        Reemplazar valores nulos o vacíos
        Convertir texto a minúsculas
        Eliminar caracteres especiales
        Corregir problemas de comillas y encoding
        Estandarizar formatos de texto
        Crear objeto Movie
        Agregar Movie a peliculasLimpias
    FIN PARA
    RETORNAR peliculasLimpias
FIN

ALGORITMO Tokenizar 
ENTRADA: texto 
SALIDA: listaPalabras 
INICIO
    Eliminar signos de puntuación
    Separar texto por espacios
    Guardar palabras en listaPalabras
    RETORNAR listaPalabras
FIN
(Pseudocódigos basados en la lógica de Limpieza de datos y Tokenización )  2. Construcción de Índices y Árboles   PlaintextALGORITMO ConstruirIndiceInvertido 
ENTRADA: palabras, indice, document_id
SALIDA: indiceActualizado
INICIO
    PARA CADA palabra EN palabras HACER
        SI palabra NO EXISTE EN indice ENTONCES
            indice[palabra] ← lista vacía
        FIN SI
        SI document_id NO EXISTE EN indice[palabra] ENTONCES
            insertar document_id EN indice[palabra]
        FIN SI
    FIN PARA
    RETORNAR indiceActualizado
FIN

ALGORITMO ConstruirSuffixTrie 
ENTRADA: texto
SALIDA: trie
INICIO
    Crear trie vacío
    PARA i ← 0 HASTA longitud(texto)-1 HACER
        sufijo ← subcadena(texto, i)
        InsertarSufijo(trie.raiz, sufijo)
    FIN PARA
    RETORNAR trie
FIN

ALGORITMO InsertarSufijo 
ENTRADA: nodo, sufijo 
SALIDA: trieActualizado
INICIO
    actual ← nodo
    PARA CADA caracter EN sufijo HACER
        SI caracter NO EXISTE EN actual.hijos ENTONCES
            actual.hijos[caracter] ← nuevo Nodo
        FIN SI
        actual ← actual.hijos[caracter]
    FIN PARA
    actual.fin ← VERDADERO
    RETORNAR trieActualizado
FIN
(Pseudocódigos basados en la construcción del Inverted Index, Suffix Tree e inserción de sufijos )  3. Procesos de Búsqueda   PlaintextALGORITMO BuscarHibrida 
ENTRADA: indice, arbolesSufijos, consulta 
SALIDA: resultados
INICIO
    palabras ← Tokenizar(consulta)
    candidatos ← BuscarPalabra(indice, palabras[0])
    resultados ← lista vacía
    PARA CADA doc_id EN candidatos HACER
        arbol ← arbolesSufijos[doc_id]
        SI ExistePatron(arbol.raiz, consulta) ENTONCES
            insertar doc_id EN resultados
        FIN SI
    FIN PARA
    RETORNAR resultados
FIN
(Pseudocódigo basado en la lógica de Búsqueda Híbrida, la cual utiliza subrutinas de Búsqueda Exacta y Parcial )  4. Sistemas de Relevancia y Recomendación   PlaintextALGORITMO CalcularRelevancia 
ENTRADA: peliculas, consulta 
SALIDA: ranking 
INICIO
    PARA CADA pelicula EN peliculas HACER
        puntaje ← 0
        SI consulta EXISTE EN pelicula.title ENTONCES
            puntaje ← puntaje + 5
        FIN SI
        SI consulta EXISTE EN pelicula.plot ENTONCES
            puntaje ← puntaje + 3
        FIN SI
        SI consulta EXISTE EN tags ENTONCES
            puntaje ← puntaje + 2
        FIN SI
        Guardar puntaje de pelicula
    FIN PARA
    Ordenar peliculas por puntaje descendente
    RETORNAR primeras 5 peliculas
FIN

ALGORITMO RecomendarPeliculas 
ENTRADA: likesUsuario, peliculas 
SALIDA: recomendaciones 
INICIO
    recomendaciones ← lista vacía
    PARA CADA peliculaLike EN likesUsuario HACER
        PARA CADA pelicula EN peliculas HACER
            SI genero SIMILAR O palabrasClave SIMILARES O sinopsis SIMILAR ENTONCES
                agregar pelicula A recomendaciones
            FIN SI
        FIN PARA
    FIN PARA
    Ordenar recomendaciones por similitud
    RETORNAR recomendaciones
FIN
(Pseudocódigos basados en el cálculo de relevancia y recomendaciones )  ⏱️ Complejidad Temporal   OperaciónComplejidadTokenización   O(n)   Inserción Inverted Index   O(k)   Búsqueda exacta   O(k)   Construcción Suffix Trie   O(n^2)   Búsqueda parcial   O(m)   Documentación generada a partir de los requerimientos de entrega del Proyecto Programación III.  

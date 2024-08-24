# CineExpertParcial1_USPG
sistema experto que recomienda películas basadas en las preferencias del usuario. Utiliza un enfoque de encadenamiento hacia adelante para filtrar opciones según género, duración y estilo, proporcionando recomendaciones precisas y personalizadas. Ideal para usuarios que buscan sugerencias de películas alineadas con sus gustos específicos.

// Base de conocimientos: lista de películas con sus atributos
const peliculas = [
    { titulo: "Inception", genero: "acción", duracion: "larga", estilo: "ciencia ficción", director: "Christopher Nolan", anio: 2010 },
    { titulo: "Parasite", genero: "drama", duracion: "media", estilo: "suspenso", director: "Bong Joon-ho", anio: 2019 },
    { titulo: "Toy Story", genero: "animada", duracion: "corta", estilo: "familiar", director: "John Lasseter", anio: 1995 },
    { titulo: "Mad Max: Fury Road", genero: "acción", duracion: "corta", estilo: "adrenalina", director: "George Miller", anio: 2015 },
    { titulo: "El Señor de los Anillos: El Retorno del Rey", genero: "fantasía", duracion: "larga", estilo: "épica", director: "Peter Jackson", anio: 2003 },
    { titulo: "Whiplash", genero: "drama", duracion: "corta", estilo: "musical", director: "Damien Chazelle", anio: 2014 }
];

// Recolección de preferencias del usuario
function obtenerPreferenciasUsuario() {
    return {
        genero: prompt("¿Qué género de película te interesa? (acción, drama, fantasía, animada, etc.)"),
        duracion: prompt("¿Preferís películas cortas, medias o largas?"),
        estilo: prompt("¿Qué estilo de película preferís? (adrenalina, ciencia ficción, épica, familiar, musical, etc.)")
    };
}

// Motor de inferencia: encadenamiento hacia adelante para buscar coincidencias
function encadenamientoHaciaAdelante(preferencias, baseDeConocimientos) {
    let recomendaciones = baseDeConocimientos;

    // Evaluación de género
    recomendaciones = recomendaciones.filter(pelicula => pelicula.genero.toLowerCase() === preferencias.genero.toLowerCase());

    // Evaluación de duración
    recomendaciones = recomendaciones.filter(pelicula => pelicula.duracion.toLowerCase() === preferencias.duracion.toLowerCase());

    // Evaluación de estilo
    recomendaciones = recomendaciones.filter(pelicula => pelicula.estilo.toLowerCase() === preferencias.estilo.toLowerCase());

    return recomendaciones;
}

// Función para recomendar película
function recomendarPelicula() {
    const preferenciasUsuario = obtenerPreferenciasUsuario();
    const peliculasRecomendadas = encadenamientoHaciaAdelante(preferenciasUsuario, peliculas);

    if (peliculasRecomendadas.length > 0) {
        console.log("Basado en tus preferencias, te recomiendo las siguientes películas:");
        peliculasRecomendadas.forEach(pelicula => {
            console.log(`- ${pelicula.titulo} (${pelicula.anio}), dirigida por ${pelicula.director}.`);
        });
    } else {
        console.log("No encontré una película que coincida exactamente con tus preferencias.");
    }
}

// Ejecución del sistema experto
recomendarPelicula();

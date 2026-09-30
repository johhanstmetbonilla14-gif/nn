import streamlit as st

# ---------------------------------------
# DATOS DE LOS COMPAÑEROS
# ---------------------------------------

companeros = [
    {
        "nombre": "Compañero 1",
        "edad": 17,
        "sexo": "masculino",
        "canciones": "reguetón y música urbana",
        "peliculas": "acción",
        "deportes": "fútbol",
        "materia": "educación física",
        "comida": "hamburguesa",
        "fortaleza": "responsabilidad",
        "debilidad": "timidez"
    },
    {
        "nombre": "Compañero 2",
        "edad": 16,
        "sexo": "masculino",
        "canciones": "pop",
        "peliculas": "comedia",
        "deportes": "fútbol",
        "materia": "matemáticas",
        "comida": "pizza",
        "fortaleza": "creatividad",
        "debilidad": "distracción"
    },
    {
        "nombre": "Compañero 3",
        "edad": 16,
        "sexo": "masculino",
        "canciones": "música urbana",
        "peliculas": "acción",
        "deportes": "baloncesto",
        "materia": "informática",
        "comida": "pollo",
        "fortaleza": "trabajo en equipo",
        "debilidad": "nervios"
    },
    {
        "nombre": "Compañero 4",
        "edad": 15,
        "sexo": "femenino",
        "canciones": "pop",
        "peliculas": "románticas",
        "deportes": "voleibol",
        "materia": "español",
        "comida": "pasta",
        "fortaleza": "creatividad",
        "debilidad": "timidez"
    },
    {
        "nombre": "Compañero 5",
        "edad": 15,
        "sexo": "femenino",
        "canciones": "pop y música urbana",
        "peliculas": "comedia",
        "deportes": "voleibol",
        "materia": "biología",
        "comida": "pizza",
        "fortaleza": "responsabilidad",
        "debilidad": "nervios"
    }
]


# ---------------------------------------
# PERSONALIDAD DEL CHATBOT
# ---------------------------------------

def crear_personalidad():
    canciones = [p["canciones"] for p in companeros]
    deportes = [p["deportes"] for p in companeros]
    fortalezas = [p["fortaleza"] for p in companeros]

    personalidad = {
        "musica": "música urbana y pop",
        "deporte": "fútbol, voleibol y baloncesto",
        "fortalezas": "responsabilidad, creatividad y trabajo en equipo",
        "personalidad": "amigable, divertida, responsable y colaboradora"
    }

    return personalidad


personalidad = crear_personalidad()


# ---------------------------------------
# RESPUESTAS DEL CHATBOT
# ---------------------------------------

def responder(mensaje):

    mensaje = mensaje.lower()

    if "hola" in mensaje or "buenas" in mensaje:
        return (
            "¡Hola! Soy el chatbot creado a partir de la información "
            "recogida en la entrevista de los compañeros."
        )

    if "música" in mensaje or "canciones" in mensaje:
        return (
            "Según las entrevistas, me gusta principalmente el pop "
            "y la música urbana."
        )

    if "película" in mensaje or "peliculas" in mensaje:
        return (
            "Las preferencias incluyen películas de acción, comedia "
            "y otros géneros."
        )

    if "deporte" in mensaje or "fútbol" in mensaje:
        return (
            "Los deportes más mencionados fueron fútbol, voleibol "
            "y baloncesto."
        )

    if "comida" in mensaje:
        return (
            "Entre las comidas mencionadas están la pizza, hamburguesa, "
            "pollo y pasta."
        )

    if "materia" in mensaje:
        return (
            "Las materias mencionadas incluyen matemáticas, informática, "
            "español, biología y educación física."
        )

    if "personalidad" in mensaje:
        return (
            "Mi personalidad combina características encontradas "
            "en las entrevistas: soy amigable, responsable, creativo "
            "y me gusta trabajar en equipo."
        )

    if "fortaleza" in mensaje or "fortalezas" in mensaje:
        return (
            "Las fortalezas más mencionadas fueron responsabilidad, "
            "creatividad y trabajo en equipo."
        )

    if "debilidad" in mensaje or "debilidades" in mensaje:
        return (
            "Algunas dificultades mencionadas fueron timidez, nervios "
            "y distracción."
        )

    if "quién eres" in mensaje or "quien eres" in mensaje:
        return (
            "Soy un chatbot desarrollado con Python y Streamlit. "
            "Mi personalidad se construyó utilizando información "
            "general de las entrevistas."
        )

    return (
        "Interesante. Puedo hablar sobre música, películas, deportes, "
        "comida, materias, fortalezas y personalidad."
    )


# ---------------------------------------
# INTERFAZ DE STREAMLIT
# ---------------------------------------

st.set_page_config(
    page_title="Chatbot de los Compañeros",
    page_icon="🤖"
)

st.title("🤖 Chatbot de los Compañeros")

st.write(
    "Este chatbot utiliza información general obtenida mediante "
    "una entrevista a cinco compañeros."
)

st.info(
    "Los datos utilizados en este ejemplo son ficticios y sirven "
    "únicamente para demostrar el funcionamiento del proyecto."
)


# ---------------------------------------
# CHAT
# ---------------------------------------

if "mensajes" not in st.session_state:
    st.session_state.mensajes = []

for mensaje in st.session_state.mensajes:

    with st.chat_message(mensaje["rol"]):
        st.write(mensaje["texto"])


pregunta = st.chat_input("Escribe una pregunta al chatbot...")

if pregunta:

    st.session_state.mensajes.append({
        "rol": "user",
        "texto": pregunta
    })

    respuesta = responder(pregunta)

    st.session_state.mensajes.append({
        "rol": "assistant",
        "texto": respuesta
    })

    st.rerun()


# ---------------------------------------
# PERSONALIDAD
# ---------------------------------------

st.sidebar.header("🧠 Personalidad")

st.sidebar.write(
    "La personalidad del chatbot fue construida a partir "
    "de las preferencias generales de los entrevistados."
)

st.sidebar.write(
    "**Características:** amigable, responsable, creativa "
    "y colaboradora."
)

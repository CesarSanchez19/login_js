<template>
    <!-- Contenedor principal para el registro -->
    <div class="register-container">
        <!-- Caja central que contiene el formulario de registro -->
        <div class="register-box">
            <!-- Título de la sección -->
            <h1 class="title">Create an Account</h1>
            <!-- Grupo de formulario para el campo de email -->
            <div class="form-group">
                <!-- Campo de entrada para el email -->
                <input type="text" placeholder="Email" v-model="email" class="input-field" />
            </div>
            <!-- Grupo de formulario para el campo de contraseña -->
            <div class="form-group">
                <!-- Campo de entrada para la contraseña -->
                <input type="password" placeholder="Password" v-model="password" class="input-field" />
            </div>
            <!-- Grupo de botones para las acciones -->
            <div class="button-group">
                <!-- Botón para registrar al usuario -->
                <button @click="register" class="submit-btn">Submit</button>
                <!-- Botón para registrarse con Google -->
                <button @click="signInWithGoogle" class="google-btn">
                    Sign In With Google
                </button>
            </div>
        </div>
    </div>
</template>
<script setup>
import { ref } from "vue"; // Importa el método ref para manejar estados reactivos
import { getAuth, createUserWithEmailAndPassword } from "firebase/auth"; // Importa métodos de Firebase Auth
import { useRouter } from "vue-router"; // Importa el enrutador de Vue para navegación

// Estado reactivo para almacenar el email ingresado
const email = ref("");
// Estado reactivo para almacenar la contraseña ingresada
const password = ref("");

// Crea una instancia del enrutador
const router = useRouter("");

// Función para registrar al usuario
const register = () => {
    // Obtiene la instancia de autenticación de Firebase
    const auth = getAuth();
    // Crea un usuario con email y contraseña utilizando Firebase Auth
    createUserWithEmailAndPassword(auth, email.value, password.value)
        .then(() => {
            alert('Successfully registered'); // Mensaje de éxito en consola
            router.push("/Feed"); // Redirige al usuario a la ruta "/Feed" tras registrarse
        })
        .catch((error) => {
            console.log(error.code); // Muestra el código de error en consola si falla
        });
};
</script>
<style scoped>
/* Estilo del contenedor principal */
.register-container {
    display: flex; /* Alinea elementos en fila */
    justify-content: center; /* Centra horizontalmente */
    align-items: center; /* Centra verticalmente */
    min-height: 100vh; /* Altura mínima del contenedor */
    padding: 20px; /* Espaciado interno */
}

/* Estilo de la caja del formulario */
.register-box {
    background-color: white; /* Fondo blanco */
    padding: 2rem; /* Espaciado interno */
    border-radius: 8px; /* Bordes redondeados */
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* Sombra para profundidad */
    width: 100%; /* Ancho completo */
    max-width: 400px; /* Ancho máximo */
}

/* Estilo del título */
.title {
    color: #333; /* Color del texto */
    font-size: 1.8rem; /* Tamaño de fuente */
    font-weight: 600; /* Peso de fuente */
    margin-bottom: 1.5rem; /* Margen inferior */
    text-align: center; /* Centrar texto */
}

/* Estilo del grupo de formulario */
.form-group {
    margin-bottom: 1rem; /* Margen inferior entre grupos */
}

/* Estilo de los campos de entrada */
.input-field {
    width: 100%; /* Ancho completo */
    padding: 0.75rem; /* Espaciado interno */
    border: 1px solid #ddd; /* Borde gris claro */
    border-radius: 4px; /* Bordes redondeados */
    font-size: 1rem; /* Tamaño de fuente */
    transition: border-color 0.3s ease; /* Transición suave al cambiar el borde */
}

/* Estilo cuando el campo está enfocado */
.input-field:focus {
    outline: none; /* Quita el contorno predeterminado */
    border-color: #4a90e2; /* Cambia el color del borde */
}

/* Estilo del grupo de botones */
.button-group {
    display: flex; /* Muestra botones en una columna */
    flex-direction: column; /* Dirección de columna */
    gap: 1rem; /* Espaciado entre botones */
    margin-top: 1.5rem; /* Margen superior */
}

/* Estilo de los botones (general) */
.submit-btn,
.google-btn {
    width: 100%; /* Ancho completo */
    padding: 0.75rem; /* Espaciado interno */
    border: none; /* Sin bordes */
    border-radius: 4px; /* Bordes redondeados */
    font-size: 1rem; /* Tamaño de fuente */
    cursor: pointer; /* Cambia el cursor al puntero */
    transition: background-color 0.3s ease; /* Transición suave al cambiar el color */
}

/* Estilo del botón de registro */
.submit-btn {
    background: linear-gradient(to right, #FF4300, #FF6400); /* Gradiente de color */
    color: white; /* Texto blanco */
}

/* Efecto hover en el botón de registro */
.submit-btn:hover {
    background-color: #357abd; /* Cambia el color de fondo */
}

/* Estilo del botón de Google */
.google-btn {
    background-color: #fff; /* Fondo blanco */
    color: #757575; /* Texto gris */
    border: 1px solid #ddd; /* Borde gris claro */
}

/* Efecto hover en el botón de Google */
.google-btn:hover {
    background-color: #f5f5f5; /* Fondo gris claro */
}
</style>

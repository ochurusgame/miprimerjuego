# Mi App Móvil - React Native + Expo & Neovim

Aplicación móvil multiplataforma desarrollada en **Ubuntu Server** utilizando **Neovim (LazyVim)** como IDE principal y visualización en tiempo real vía **Expo Go**.

## Requisitos Previos

- **Node.js**: v20+ / NVM
- **Expo CLI** & **EAS CLI**
- **Token de Expo**: Configurado en la variable `EXPO_TOKEN`
- **Expo Go**: Instalado en el dispositivo móvil (iOS / Android)

##   Flujo de Desarrollo Diario

### 1. Iniciar el servidor de desarrollo (Terminal 1)
```bash
cd ~/mi-app-movil
npx expo start --tunnel

2. Editar código en tiempo real (Terminal 2)
cd ~/mi-app-movil
nvim .

⌨️ Atajos Clave en Neovim (LazyVim)

Espacio + f + f: Buscar y abrir archivos (App.tsx, index.ts, etc.)

Espacio + e: Abrir/Cerrar el explorador de archivos lateral

:w: Guardar cambios y recargar la app en vivo en Expo Go

:q: Salir de Neovim

4. Presiona **`Esc`**, escribe **`:wq`** y presiona **`Enter`** para guardar.

---

### 3. Conectar y Subir tu Proyecto a GitHub

1. Entra a **[GitHub.com](https://github.com)** desde tu navegador web y crea un nuevo repositorio llamado **`mi-app-movil`** (déjalo **sin** marcar la casilla de "Add a README file")[cite: 1].
2. Copia la URL de tu repositorio de GitHub (ejemplo: `[https://github.com/tu-usuario/mi-app-movil.git](https://github.com/tu-usuario/mi-app-movil.git)`)[cite: 1].
3. En tu terminal de Ubuntu Server (dentro de `~/mi-app-movil`), ejecuta los siguientes comandos en orden[cite: 1]:

```bash
# 1. Inicializar el repositorio Git
git init
git branch -M main

# 2. Preparar y realizar el primer commit
git add .
git commit -m "feat: configuracion inicial del entorno React Native + Expo con Neovim"

# 3. Vincular con GitHub (reemplaza con la URL de tu repositorio)
git remote add origin https://github.com/tu-usuario/mi-app-movil.git

# 4. Subir el código a GitHub
git push -u origin main

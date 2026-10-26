# 📱 Entorno de Desarrollo Móvil: React Native + Expo + Neovim en Ubuntu Server

Documentación técnica completa del entorno de desarrollo móvil virtualizado utilizando **Ubuntu Server**, **Neovim (LazyVim)** como IDE en terminal, servidor de túneles **Expo Go** para pruebas en tiempo real en dispositivos móviles (iOS/Android) y control de versiones con **GitHub**.

---

## 🛠️ 1. Arquitectura e Instalación del Entorno Base

### 🖥️ Máquina Virtual (VirtualBox)
- **SO**: Ubuntu Server 22.04 / 24.04 LTS
- **Recursos**: 4 GB+ RAM, 2 CPUs, 30 GB+ SSD
- **Red**: Adaptador en modo NAT / Puente con reenvío de puertos SSH (Puerto `22`).

### 🔑 SSH y Conexión Remota desde Windows
Para conectar tu terminal física a la máquina virtual:
```bash
ssh dev@<IP_SERVIDOR_UBUNTU>

🚀 2. Instalación de Dependencias EsencialesComponentes de Desarrollo en Ubuntu ServerBash# Update del sistema y herramientas de compilación
sudo apt update && sudo apt upgrade -y
sudo apt install -y build-essential curl wget git unzip xclip ripgrep fd-find python3 python3-pip android-tools-adb scrcpy xdg-utils

# Instalación de Neovim v0.10+ (Binario oficial)
curl -LO [https://github.com/neovim/neovim/releases/download/stable/nvim-linux-x86_64.tar.gz](https://github.com/neovim/neovim/releases/download/stable/nvim-linux-x86_64.tar.gz)
tar -xzf nvim-linux-x86_64.tar.gz
sudo cp -r nvim-linux-x86_64/* /usr/local/
rm -rf nvim-linux-x86_64*

# Instalación de Node.js LTS vía NVM
curl -o- [https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh](https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh) | bash
source ~/.bashrc
nvm install --lts

# Instalación de CLI de Expo y EAS
npm install -g eas-cli

🎨 3. IDE de Terminal: Neovim con LazyVimConfiguración Inicial de LazyVimBash# Configurar la plantilla oficial de LazyVim
git clone [https://github.com/LazyVim/starter](https://github.com/LazyVim/starter) ~/.config/nvim
rm -rf ~/.config/nvim/.git

⌨️ Atajos Clave en Neovim (LazyVim)AtajoAcciónSpace + f + fBuscar y abrir archivos en el proyectoSpace + eAbrir / Ocultar el explorador de archivos lateral:w + EnterGuardar cambios (Recarga la app en tiempo real)Esc $\rightarrow$ :wqGuardar y salir de Neovim a la terminalEsc $\rightarrow$ ZZAtajo rápido para guardar y salirq (en modo normal)Cancela la grabación de macros📲

4. Autenticación y Servidor de Desarrollo Expo GoAutenticación Permanente de ExpoPara mantener activa la sesión con la cuenta de Expo en el servidor:Bashecho 'export EXPO_TOKEN="TU_EXPO_PERSONAL_ACCESS_TOKEN"' >> ~/.bashrc
source ~/.bashrc
Iniciar el Servidor con TúnelBashcd ~/mi-app-movil
npx expo start --tunnel
Abre la app Expo Go en tu iPhone/Android o la app Cámara para escanear el código QR.🐙 5. Control de Versiones e Integración con GitHubConfiguración Global de GitBashgit config --global user.name "ochurusgame"
git config --global user.email "@gmail.com"
Conexión con Token de Acceso Personal (PAT)Bashgit remote set-url origin [https://ochurusgame:TU_PERSONAL_ACCESS_TOKEN_GITHUB@github.com/ochurusgame/miprimerjuego.git](https://ochurusgame:TU_PERSONAL_ACCESS_TOKEN_GITHUB@github.com/ochurusgame/miprimerjuego.git)

🔄 6. Flujo de Trabajo Diario (Paso a Paso)Cuando te sientes a programar cada día:Terminal 1 (Servidor Expo):Bashcd ~/mi-app-movil
npx expo start --tunnel
Terminal 2 (Editor Neovim):Bashcd ~/mi-app-movil
nvim .
Dispositivo Móvil: Abre la app Expo Go para ver todos los cambios reflejados en tiempo real al presionar :w en Neovim.Guardar cambios en GitHub al finalizar:Bashgit add .
git commit -m "feat: avances en desarrollo"
git push origin main

---

### ¿Cómo actualizar este README directamente en GitHub?

1. En la página web de tu repositorio en GitHub donde estás parado (imagen), presiona la caja del `README` o haz clic en el ícono de **lápiz ✏️** (arriba a la derecha del recuadro del README).
2. Borra todo el texto existente y pega el bloque Markdown anterior.
3. Haz clic en el botón verde **"Commit changes..."** arriba a la derecha.

¡Y listo! Tendrás tu portafolio y repositorio documentado a nivel profesional.

# 3. Vincular con GitHub (reemplaza con la URL de tu repositorio)
git remote add origin https://github.com/tu-usuario/mi-app-movil.git

# 4. Subir el código a GitHub
git push -u origin main

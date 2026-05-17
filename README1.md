# Guía paso a paso para poner en funcionamiento el proyecto `scouter_lol`

Esta guía resume todo el proceso realizado para ejecutar correctamente el proyecto de Django con TensorFlow en una máquina virtual de Ubuntu usando VirtualBox.

---

# 1. Crear la máquina virtual en VirtualBox

Crear una VM de Ubuntu con:
- mínimo 8 GB RAM recomendados
- mínimo 60 GB de disco dinámico
- virtualización habilitada:
  - VT-x/AMD-V
  - Paginación anidada

---

# 2. Compartir la carpeta del proyecto desde Windows

En VirtualBox:

```text
Configuración → Carpetas compartidas
```

Agregar la carpeta del proyecto de Windows:
- activar:
  - Automontar
  - Hacer permanente

---

# 3. Instalar Guest Additions

Dentro de Ubuntu:

```bash
sudo apt update

sudo apt install build-essential dkms linux-headers-$(uname -r)
```

Luego en VirtualBox:

```text
Dispositivos → Insertar imagen de CD de las Guest Additions
```

Ejecutar:

```bash
sudo /media/$USER/VBox_GAs*/VBoxLinuxAdditions.run
```

Reiniciar:

```bash
sudo reboot
```

---

# 4. Dar permisos a la carpeta compartida

```bash
sudo usermod -aG vboxsf $USER
```

Reiniciar nuevamente:

```bash
sudo reboot
```

---

# 5. Instalar herramientas básicas

```bash
sudo apt update

sudo apt install git python3-pip python3-venv python3-full
```

---

# 6. Instalar Miniconda

Descargar Miniconda para Linux x86_64.

Ir a Descargas:

```bash
cd ~/Downloads
```

Instalar:

```bash
bash Miniconda3-latest-Linux-x86_64.sh
```

Aceptar:
- ENTER
- yes

Cargar Conda:

```bash
source ~/.bashrc
```

---

# 7. Crear entorno virtual compatible con TensorFlow

Crear entorno Conda con Python 3.11:

```bash
conda create -n ia python=3.11
```

Activar entorno:

```bash
conda activate ia
```

Verificar que aparezca:

```text
(ia)
```

---

# 8. Ir a la carpeta del proyecto

Ejemplo:

```bash
cd ~/Desktop/sf_django_deep_learning/scouter_lol
```

Verificar que exista `manage.py`:

```bash
ls
```

---

# 9. Instalar Django

```bash
pip install Django==4.1
```

Verificar versión:

```bash
python -m django --version
```

---

# 10. Instalar dependencias del proyecto

Instalar librerías necesarias:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn pillow opencv-python tensorflow
```

---

# 11. Aplicar migraciones

```bash
python manage.py migrate
```

---

# 12. Ejecutar el servidor

```bash
python manage.py runserver
```

Si todo funciona aparecerá:

```text
Starting development server at http://127.0.0.1:8000/
```

---

# 13. Abrir el proyecto en el navegador

Entrar a:

```text
http://127.0.0.1:8000/
```

---

# 14. Detener el servidor

En terminal:

```text
CTRL + C
```

---

# 15. Activar nuevamente el entorno en futuras sesiones

Cada vez que abras Ubuntu:

```bash
conda activate ia
```

Luego:

```bash
cd ~/Desktop/sf_django_deep_learning/scouter_lol
```

y finalmente:

```bash
python manage.py runserver
```

---

# Problemas solucionados durante el proceso

Se resolvieron:
- errores de permisos de VirtualBox
- falta de espacio en disco
- incompatibilidades de TensorFlow
- errores `externally-managed-environment`
- errores de `pip`
- incompatibilidades con Python 3.13/3.14
- errores `illegal hardware instruction`
- dependencias faltantes (`seaborn`, `sklearn`, etc.)

---

# Recomendación final

Para proyectos de:
- IA
- CNN
- TensorFlow
- Django

es más estable usar:
- Ubuntu
- Conda
- Python 3.11

en lugar de Kali Linux.


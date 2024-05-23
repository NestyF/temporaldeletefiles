# Script de Limpieza de Sistema en Kali Linux

Este script realiza varias tareas de limpieza en tu sistema Kali Linux para liberar espacio en disco.

## Instrucciones de Uso

1. **Crear el Script**: Crea un archivo llamado `clean_system.sh`.

    ```sh
    nano clean_system.sh
    ```

2. **Copiar el Código**: Copia y pega el siguiente código en el archivo `clean_system.sh`.

    ```bash
    #!/bin/bash

    # Limpiar la caché de paquetes descargados
    sudo apt clean

    # Eliminar paquetes huérfanos
    sudo apt autoremove -y

    # Limpiar la caché de archivos temporales
    sudo rm -rf /tmp/*

    # Limpiar la caché de logs de systemd
    sudo journalctl --vacuum-size=50M

    # Eliminar archivos de la carpeta de caché de aplicaciones
    sudo rm -rf ~/.cache/*

    # Eliminar miniaturas de imágenes antiguas
    rm -rf ~/.thumbnails/*

    # Eliminar archivos de la papelera de reciclaje
    rm -rf ~/.local/share/Trash/*

    # Eliminar paquetes no esenciales
    sudo apt-get remove (dpkg−query−f′(dpkg-query -f '{binary:Package}\n' -W '*' | grep -vE '^gimp-.*′|grep−v′firefox−.∗' | grep -v '^firefox-.*' | grep -v '^chromium-.*′|grep−v′libreoffice−.∗' | grep -v '^libreoffice-.*' | grep -v '^kali-.*′|grep−v′python3.∗' | grep -v '^python3.*' | grep -v '^ruby.*$')

    # Eliminar paquetes huérfanos restantes y sus configuraciones
    sudo apt-get autoremove --purge

    # Eliminar archivos .deb en caché
    sudo rm -rf /var/cache/apt/archives/*.deb

    # Buscar y eliminar archivos .deb en todo el sistema
    sudo find / -name "*.deb" -type f -exec rm -rf {} \;

    # Mostrar el espacio en disco después de la limpieza
    echo "Espacio en disco después de la limpieza:"
    df -h /dev/sda1
    ```

3. **Guardar y Cerrar**: Guarda el archivo y cierra el editor de texto.

4. **Hacer el Script Ejecutable**: Haz que el script sea ejecutable.

    ```sh
    chmod +x clean_system.sh
    ```

5. **Ejecutar el Script**: Ejecuta el script.

    ```sh
    ./clean_system.sh
    ```

## Explicación del Script

- **Limpiar la Caché de Paquetes Descargados**: `sudo apt clean` limpia la caché de los paquetes descargados.
- **Eliminar Paquetes Huérfanos**: `sudo apt autoremove -y` elimina los paquetes huérfanos.
- **Limpiar la Caché de Archivos Temporales**: `sudo rm -rf /tmp/*` elimina todos los archivos temporales.
- **Limpiar la Caché de Logs de Systemd**: `sudo journalctl --vacuum-size=50M` reduce el tamaño de los logs de systemd.
- **Eliminar Archivos de la Carpeta de Caché de Aplicaciones**: `sudo rm -rf ~/.cache/*` elimina todos los archivos de caché de aplicaciones.
- **Eliminar Miniaturas de Imágenes Antiguas**: `rm -rf ~/.thumbnails/*` elimina todas las miniaturas de imágenes antiguas.
- **Eliminar Archivos de la Papelera de Reciclaje**: `rm -rf ~/.local/share/Trash/*` elimina todos los archivos de la papelera de reciclaje.
- **Eliminar Paquetes No Esenciales**: Elimina paquetes no esenciales excepto algunos como `gimp`, `firefox`, `chromium`, `libreoffice`, `kali`, `python3`, y `ruby`.
- **Eliminar Paquetes Huérfanos Restantes y Sus Configuraciones**: `sudo apt-get autoremove --purge` elimina cualquier paquete huérfano restante y sus configuraciones.
- **Eliminar Archivos .deb en Caché**: `sudo rm -rf /var/cache/apt/archives/*.deb` elimina todos los archivos .deb en caché.
- **Buscar y Eliminar Archivos .deb en Todo el Sistema**: `sudo find / -name "*.deb" -type f -exec rm -rf {} \;` busca y elimina todos los archivos .deb en el sistema.
- **Mostrar el Espacio en Disco Después de la Limpieza**: `df -h /dev/sda1` muestra el espacio en disco después de la limpieza.

Este script te ayudará a mantener tu sistema Kali Linux limpio y con espacio libre en el disco.

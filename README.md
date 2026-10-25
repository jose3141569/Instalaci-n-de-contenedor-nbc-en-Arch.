# Instalación de contenedor-nbc-en-Arch.
En este repositorio es mostrar como instale nbc, para poder compilar bloques de NXT de lego.
Para crear un contenedor de forma fácil en la distribución de Arch Linux se deben instalar los siguientes paquetes: distrobox,podman y flatpak.
Los pasos que realice fueron los siguientes:

```bash

#!/bin/bash
echo "Actualizar Sistema..."
sleep 2
sudo pacman -Syu --noconfirm
echo "Descargar paquetes necesarios..."
sleep 2
sudo pacman -S --noconfirm podman distrobox fuse-overlayfs flatpak 
echo "Hacer que podman use a distrobox sin root.."
sleep 3
//Esta parte es para que podman pueda trabar sin la necesidad de usar root. El comando viene de la pagina oficial de Arch. 
sudo usermod --add-subuids 100000-165535 --add-subgids 100000-165535 $SUDO_USER  //$SUDO_USER es para mandarlo al usuario al no al root.
echo "Espere un momento.."
sleep 2
echo "Actualizar podman al usuario original.."
sleep 2
sudo -u "$SUDO_USER" podman system migrate
sleep 2
echo "El sistema debe reiniciar..."
sleep 2
sudo reboot  //Reiniciar el sistema para flatpak y cambios que se realizaron.
```

Lo anterior lo ejecute como * sudo ./<Nombre_archivo> * ya que este codigo de bash era  para otra maquina. El siguiente codigo se hizo para poder instalar nbc y distroshelf.

```bash
#!/bin/bash
flatpak update -y
flatpak install -y com.ranfdev.DistroShelf
cd //mandarte a la carpeta home
echo "Creando carpeta..."
mkdir -p nbc
sleep 2
echo "Entrando a carpeta.."
cd nbc/ || exit //sino se creo sale del programa
sleep 2
echo "Descargar archivo nbc en sourceforge"
sleep 2
wget -O nbc-1.2.1.r4.tgz "https://sourceforge.net/projects/bricxcc/files/NBC_NXC/NBC%20release%201.2.1%20r4/nbc-1.2.1.r4.tgz/download?use_mirror=master"
echo "Descomprimir..."
sleep 2
tar -xvzf nbc-1.2.1.r4.tgz
echo "Eliminar nbc-1.2.1.r4.tgz ..."
rm nbc-1.2.1.r4.tgz
sleep 2
echo "Finalizado. Seguir con Distroshielf  TT_TT."
sleep 2
exit
```
El bash anterior lo ejecutas como  *./<nombre_archivo>. (Nota que no use el sudo aquí)* Recuerda que ambos archivos debes darles permisos de ejecución con el comando *chmos +x <nombre_archivo>*.

Para crear un contenedor ingresa a Distrishlelf y dale click al simbolo de mas.

<img width="248" height="49" alt="Image" src="https://github.com/user-attachments/assets/6f98db7d-89c4-4b9b-8b72-171f7e8da6aa" />

Se abre una nueva ventana y le das un nombre al contenedor que quieres y buscas la imagen de la misma. En mi caso por el idioma en ingles es *Base image*

<img width="949" height="686" alt="Image" src="https://github.com/user-attachments/assets/b2f2d130-e12c-446f-944a-30a0d60ec600" />

En mi caso las opciones que viene no me interesan pero si es tu caso que las necesitas activalas.
Al estarse creando aparece lo siguiente:

<img width="352" height="649" alt="Image" src="https://github.com/user-attachments/assets/ec30d788-b728-4861-ad24-d43f25953bac" />

Nuestro interes es debian en mi caso instale debian 13 y al terminar de instalarse el contenedor veremos lo siguiente: 

<img width="886" height="693" alt="Image" src="https://github.com/user-attachments/assets/5bf244b3-0a69-4d9c-bc82-e45164113829" />

Para abir el contenedor es con la mini terminal que tiene en la parte de status.
 
y se vera lo siguiente:  

<img width="871" height="655" alt="Image" src="https://github.com/user-attachments/assets/e00fc306-0907-4c3f-b883-f4c5bbf4e20e" />

en caso de que no abra la terminal busca en opciones la terminal que tienes instalada.

<img width="892" height="687" alt="Image" src="https://github.com/user-attachments/assets/ed95d75d-929d-4242-820a-d241e141f7b7" />

<img width="899" height="691" alt="Image" src="https://github.com/user-attachments/assets/fbce0984-e9f0-477a-ad7e-fc8e42590ff9" />

En nuestra terminal actualizamos y descgarmos el paquete nbc.

<img width="1366" height="738" alt="Image" src="https://github.com/user-attachments/assets/37ff0421-37ae-4323-8dde-e6d0a429840f" />
nota que al usar *nbc -help* nos muestra que el paquete esta instalado.Por lo tanto ya tienes en tu contenedor la aplicación para usar nbc.

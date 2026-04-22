Despliegue de PokéDex en Azure Static Web Apps
Este documento describe paso a paso el proceso de despliegue de la aplicación PokéDex en Microsoft Azure, utilizando el servicio Azure Static Web Apps con integración continua desde GitHub.

1. Requisitos previos

Cuenta de estudiante en Azure for Students
Cuenta de GitHub con el repositorio pokedex creado
Git instalado localmente
Editor de código (Visual Studio Code recomendado)
Código fuente del proyecto Angular en el repositorio


2. Preparación del repositorio local
2.1. Clonado del código fuente base
El código base se obtuvo del repositorio académico y se extrajo el proyecto Angular:
bashgit clone https://github.com/rcuello/ac4dem1a.git temp-origen
cp -r temp-origen/sistemas-distribuidos/poke-dex-lab/source/pokedex-angular/. ./
rm -rf temp-origen
2.2. Inicialización del repositorio local
bashgit init
git branch -M main
git remote add origin https://github.com/Cam-lo/pokedex.git
# 💾 Webpack
<h2>🤔 ¿Qué es Webpack?</h2>
  <h4>Ideas/conceptos claves</h4>
Module bundlers son herramientas de frontend que nos permiten usar archivos con módulos JavaScript, entre otras características y convertiros a un JavaScript el cual el navegador pueda entender

  <h4>Apuntes</h4> 
 Webpack es una herramienta que nos permite preparar nuestro código para llevarlo a producción (module bundler)
 Webpack nos permite trabajar con:
  
  - HTML
  - CSS
  - JavaScript
  - Archivos estáticos
  - Imágenes
  - Fuentes
 
  Tambien nos permite tener un modo en desarrollo para nuestros proyectos para hacer pruebas
  Nacio en el 2012, desde ese entonces varias empresas lo usan como:
  
  - Twitter
  - Instagram
  - PayPal
 
  También nos permite
  
  - Gestionar dependencias
  - Ejecutar tareas
  - Conversión de archivos
  
  Nos permite trabajar en módulos
  
  - Permitiéndonos tener un código separado en desarrollo, pero en producción en una fuente
  - Webpack permite tener módulos de JS en formato
      - AMD
      - Common JS
      - ES15
    
  RESUMEN: Webpack es un module bundler que nos permite trabajar con una variedad de tecnologías web empezando desde HTML y terminando con JS. Además de tener soporte para archivos estáticos
  
<h2>🧐 Conseptos basicos</h2>

  **Webpack** es un paquete de módulos estáticos para aplicaciones de JS modernas

  **Loader** Te permite hacer un bundle de cualquier recurso estático más allá de JavaScript

  **Plugins** Extienden recursos para añadir configuraciones y particularidades de recursos externos

<h4>Apuntes</h4>
  
- Webpack construye un gráfico de dependencias que mapea cada módulo para con verlo en uno o más módulos
- Desde webpack 4 ya no dependemos de tener un archivo de configuración, pero si debemos tener un punto de entrada
- Tambien tendremos que tener un punto de salida
    - En este punto se creará nuestro proyecto una vez esté preparado
    - Normalmente es la carpeta dist ⇒ Distribution
 
- Tambien contamos con diferentes modos
    - Modo de desarrollo
    - Modo de producción
    - Modos de performance
      - Donde tu añades
        - Configuraciones de minificación
        - Donde se va enviar
        - Carpeta de destino
    - Modos de desarrollo local
      - Donde puedes
        - Crear puertos específicos para tu proyecto
        - Ver cambios en tiempo real
      
- Dispone de loader y plugins permitiéndonos preparar particularidades de nuestro proyecto

<h2>👷‍♂️ Creando un build con webpack</h2>

 - creamos una carpeta desde la terminal con mkdir y luego entramos a ella con cd (le podemos dar cualquier nombre)

```cmd
mkdir curso-webpack
cd curso webpack
```
- una vez que entres a la carpeta inicializamos nuestro repositorio con git

```git
git init
```
- El paso que sigue es inicializar nuestro proyecto con npm 

```npm
npm init -y
```

- y para abrir el proyecto como flash es poner en la terminal y les abre el editor ( si usas VS CODE) 

```cmd
code .
```
- La carpeta SRC es el source de todo el proyecto ( index.js , imágenes, utils, assets, helpers, database, etc).

<h4>Instalación de Webpack</h4>

```npm
npm i webpack webpack-cli -D
```
- Y luego ejecutamos webpack npx lo que hace es ejecutar paquetes directamente de npm, este viene instalado de npm

```npm
npx webpack
```
- Al hacer esto webpack creo una carpeta llamada dist, esto lo hace por defecto webpack sin preguntarnos.

<h4>Modo de desarrollo</h4>

- Por defecto webpack al compilar nuestro proyecto setea el modo “production” implícitamente pero podemos definirle el modo explícitamente corriendo:

```npm
npx webpack --mode production
npx webpack --mode development
```
- La diferencia radica que el modo development deja el código mas legible para los desarrolladores pero con comentarios, el modo production deja el código comprimido y mas limpio para usarse.













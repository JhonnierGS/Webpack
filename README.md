# 💾 Webpack

# Tabla de contenido

  1. [¿Qué Webpack?](#qué-es-webpack).
  2. [Conseptos](#Conseptos-basicos).
  3. [Creando un build con webpack](#Creando-un-build-con-webpack).
  4. [Babel Loader para JavaScript](#Babel-Loader-para-JavaScript).
  5. [HTML en Webpack](#HTML-en-Webpack).
  6. [Loaders para CSS y preprocesadores de CSS](#Loaders-para-CSS-y-preprocesadores-de-CSS).
  7. [Copia de archivos con webpack](#Copia-de-archivos-con-webpack).
  8. [Loaders de imagenes](#loaders-de-imagenes).
  9. [Loaders de fuentes](#loaders-de-fuentes).
  10. [optimización](#optimización:-hashes-compresión-y-minificación-de-archivos).
  11. [avegadores y dispositivos](#avegadores-y-dispositivos).

### 🤔¿Qué es Webpack?
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
  
### 🧐Conseptos basicos

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

<h2>⚙ Configuracion de webpack.config.js</h2>
  
  - El archivo de configuración nos va ayudar a poder establecer la configuración y elementos que vamos a utilizar
  - Para poder crear el archivo de configuración en la raíz del proyecto creamos un archivo llamado **webpack.config.js**
  - En el mismo debemos decir
    - El punto de entrada
    - Hacia a donde a enviar la configuración de nuestro proyecto
    - Las extensiones que vamos usar 

```javascript
const path = require('path');

module.exports = {
  // Entry nos permite decir el punto de entrada de nuestra aplicación
  entry: "./src/index.js",
  // Output nos permite decir hacia dónde va enviar lo que va a preparar webpacks
  output: {
    // path es donde estará la carpeta donde se guardará los archivos
    // Con path.resolve podemos decir dónde va estar la carpeta y la ubicación del mismo
    path: path.resolve(__dirname, "dist"),
    // filename le pone el nombre al archivo final
    filename: "main.js"
  },
  resolve: {
    // Aqui ponemos las extensiones que tendremos en nuestro proyecto para webpack los lea
    extensions: [".js"]
  },
}
```

- El flag **—config** indica donde estará nuestro archivo de configuración

```cmd
npx webpack --mode production --config webpack.config.js
```

- Para poder hacerlo más amigable el comando puedes crear un script en **package.json**

```JSON
"scripts": {
		...
    "build": "webpack --mode production --config webpack.config.js"
  },
```

**RESUMEN:** Puedes crear un archivo webpack.config.js en el cual estarán las configuraciones con las cuales webpack trabajara, entre ellas están los puntos de entrada y salida, extensiones de archivos, entre otras características 

<h2>💛 Babel Loader para JavaScript</h2>

 - Babel te permite hacer que tu código JavaScript sea compatible con todos los navegadores
 - Debes agregar a tu proyecto las siguientes dependencias

```npm
npm install -D babel-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime
```

- babel-loader nos permite usar babel con webpack
- @babel/core es babel en general
- @babel/preset-env trae y te permite usar las ultimas características de JavaScript
- @babel/plugin-transform-runtime te permite trabajar con todo el tema de asincronismo como ser **async** y **await**
- Debes crear el archivo de configuración de babel el cual tiene como nombre **.babelrc**

```babel
{
  "presets": [
    "@babel/preset-env"
  ],
  "plugins": [
    "@babel/plugin-transform-runtime"
  ]
}
```

- Para comenzar a utilizar webpack debemos agregar la siguiente configuración en **webpack.config.js**

```javascript
{
...,
module: {
    rules: [
      {
        // Test declara que extensión de archivos aplicara el loader
        test: /\.js$/,
        // Use es un arreglo u objeto donde dices que loader aplicaras
        use: {
          loader: "babel-loader"
        },
        // Exclude permite omitir archivos o carpetas especificas
        exclude: /node_modules/
      }
    ]
  }
}
```

**RESUMEN:** Babel te ayuda a transpilar el código JavaScript, a un resultado el cual todos los navegadores lo puedan entender y ejecutar. Trae “extensiones” o plugins las cuales nos permiten tener características más allá del JavaScript común

<h2>🧡 HTML en Webpack</h2>

- Es un plugin que nos facilita la tarea de enlazar los bundles a nuestro template HTML

### Instalación

```npm
npm install html-webpack-plugin -D
```

- A nuestra sección de webpack-config.js le agregamos la nueva configuración del plugin

```javascript
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
    mode: 'production', // LE INDICO EL MODO EXPLICITAMENTE
    entry: './src/index.js', // el punto de entrada de mi aplicación
    output: { // Esta es la salida de mi bundle
        path: path.resolve(__dirname, 'dist'),
        // resolve lo que hace es darnos la ruta absoluta de el S.O hasta nuestro archivo
        // para no tener conflictos entre Linux, Windows, etc
        filename: 'main.js', 
        // EL NOMBRE DEL ARCHIVO FINAL,
    },
    resolve: {
        extensions: ['.js'] // LOS ARCHIVOS QUE WEBPACK VA A LEER
    },
    module: {
        // REGLAS PARA TRABAJAR CON WEBPACK
        rules : [
            {
                test: /\.m?js$/, // LEE LOS ARCHIVOS CON EXTENSION .JS,
                exclude: /node_modules/, // IGNORA LOS MODULOS DE LA CARPETA
                use: {
                    loader: 'babel-loader'
                }
            }
        ]
    },
    // SECCION DE PLUGINS
    plugins: [
        new HtmlWebpackPlugin({ // CONFIGURACIÓN DEL PLUGIN
            inject: true, // INYECTA EL BUNDLE AL TEMPLATE HTML
            template: './public/index.html', // LA RUTA AL TEMPLATE HTML
            filename: './index.html' // NOMBRE FINAL DEL ARCHIVO
        })
    ]
}
```

<h2>💙 Loaders para CSS y preprocesadores de CSS</h2>

### ideas y conceptos claves
Un preprocesador CSS es un programa que te permite generar CSS a partir de la syntax única del preprocesador. Existen varios preprocesadores CSS de los cuales escoger, sin embargo, la mayoría de preprocesadores CSS añadirán algunas características que no existen en CSS puro, como variable, mixins, selectores anidados, entre otros. Estas características hacen la estructura de CSS más legible y fácil de mantener.

post procesadores son herramientas que procesan el CSS y lo transforman en una nueva hoja de CSS que le permiten optimizar y automatizar los estilos para los navegadores actuales.

- Para dar soporte a CSS en webpack debes instalar los siguientes paquetes

```npm
npm i mini-css-extract-plugin css-loader -D
```

- css-loader ⇒ Loader para reconocer CSS
- mini-css-extract-plugin ⇒ Extrae el CSS en archivos
- Para comenzar debemos agregar las configuraciones de webpack

```javascript
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
	...,
	module: {
    rules: [
      {
        test: /\.(css|styl)$/i,
        use: [
          MiniCssExtractPlugin.loader,
          "css-loader",
        ]
      }
    ]
  },
  plugins: [
		...
    new MiniCssExtractPlugin(),
  ]
}
```

- Si deseamos posteriormente podemos agregar herramientas poderosas de CSS como ser:
	-  **pre procesadores**
		-  Sass
		- Less
		- Stylus
	-  **post procesadores**
		-  Post CSS

**RESUMEN:** Puedes dar soporte a CSS en webpack mediante loaders y plugins, además que puedes dar superpoderes al mismo con las nuevas herramientas conocidas como pre procesadores y post procesadores


<h2>📁 Copia de archivos con webpack</h2>

- Si tienes la necesidad de mover un archivo o directorio a tu proyecto final podemos usar un plugin llamado **“copy-webpack-plugin”**
- Para instalarlo debemos ejecutar el comando

```npm
npm install copy-webpack-plugin -D
```

- ara poder comenzar a usarlo debemos agregar estas configuraciones a **webpack.config.js**

```
...javascript
const CopyPlugin = require('copy-webpack-plugin');

module.exports = {
	...
  plugins: [
    new CopyPlugin({
      patterns: [
        {
          from: path.resolve(__dirname, "src", "assets/images"),
          to: "assets/images"
        }
      ]
    }),
  ]
}
```

- Es importante las propiedades from y to
	- From ⇒ que recurso (archivo o directorio) deseamos copiar al directorio final
	- To ⇒ en que ruta dentro de la carpeta final terminara los recursos


<h2>🌆 Loaders de imagenes</h2>

- Puedes usar una forma de importar las imágenes haciendo un import de las mismas y generando una variable
- No es necesario instalar ninguna dependencia, webpack ya lo tiene incluido debemos agregar la siguiente configuración

```javascript
module.exports = {
	...
  module: {
    rules: [
      {
        test: /\.png/,
        type: "asset/resource"
      }
    ]
  },
}
```

- Para empezar a usar esta configuración debemos importar la imagen de la siguiente forma

```javascript
import github from '../assets/images/github.png';
```

Para incluirlo en el HTML debes hacer lo siguiente

```javascript
// Ejemplo en Vanilla JS
const imagen = `<img src=`${github}` />`;
```

<h2>🔠 Loaders de fuentes</h2>

- Cuando utilizamos fuentes externas una buena práctica es descargarlas a nuestro proyecto
	- Debido a que no hara un llamado a otros sitios
- Por ello es importante usarlo dentro de webpack
- Para esta tarea instalaras y usaras “file-loader” y “url-loader”

```NPM
npm install url-loader file-loader -D
```

- Para aplicar esta configuración debes agregar la siguiente información

```javascript
module.exports = {
	...
  module: {
    rules: [
			...
      {
        test: /\.(woff|woff2)$/,
        use: {
          loader: "url-loader",
          options: {
            // limit => limite de tamaño
            limit: 10000,
            // Mimetype => tipo de dato
            mimetype: "application/font-woff",
            // name => nombre de salida
            name: "[name].[ext]",
            // outputPath => donde se va a guardar en la carpeta final
            outputPath: "./assets/fonts/",
            publicPath: "./assets/fonts/",
            esModule: false,
          }
        }
      }
    ]
  },
	...
}
```

- Es importante que dentro de los estilos agregues @font-face

```css
@font-face {
	font-family: "Ubuntu";
	src: url("../assets/fonts/ubuntu-regular.woff2") format('woff2'),
			 url("../assets/fonts/ubuntu-regular.woff") format('woff');
	font-weight: 400;
	font-style: normal;
}
```

<h2>🏗 optimización: hashes, compresión y minificación de archivos</h2>

- Unos de las razones por que utilizamos webpack es porque nos permite optimizar y comprimir nuestro proyecto
- Debes utilizar los siguientes paquetes
	- css-minimizer-webpack-plugin ⇒ Nos ayuda a comprimir nuestros archivos finales CSS
	- terser-webpack-plugin ⇒ Permite minificar de una mejor forma

```NPM
npm i css-minimizer-webpack-plugin terser-webpack-plugin -D
```

- Una vez instalado el plugin debemos agregar la siguiente configuración

```javascript
...
const CssMinimizerPlugin = require('css-minimizer-webpack-plugin');
const TerserPlugin = require('terser-webpack-plugin');

module.exports = {
	...
	optimization: {
    minimize: true,
    minimizer: [
      new CssMinimizerPlugin(),
      new TerserPlugin()
    ]
  }
}
```

- Cuando nombremos en la configuración de webpack es importante usar [contenthash] para evitar problemas con la cache

























































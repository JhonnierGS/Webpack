# 馃捑 Webpack

# Tabla de contenido

  1. [驴Qu茅 Webpack?](#qu茅-es-webpack).
  2. [Conseptos](#Conseptos-basicos).
  3. [Creando un build con webpack](#Creando-un-build-con-webpack).
  4. [Babel Loader para JavaScript](#Babel-Loader-para-JavaScript).
  5. [HTML en Webpack](#HTML-en-Webpack).
  6. [Loaders para CSS y preprocesadores de CSS](#Loaders-para-CSS-y-preprocesadores-de-CSS).
  7. [Copia de archivos con webpack](#Copia-de-archivos-con-webpack).
  8. [Loaders de imagenes](#loaders-de-imagenes).
  9. [Loaders de fuentes](#loaders-de-fuentes).
  10. [optimizaci贸n](#optimizaci贸n-hashes-compresi贸n-y-minificaci贸n-de-archivos).
  11. [alias](#Webpack-Alias).
  12. [Variables de entorno](#Variables-de-entorno).
  13. [Webpack watch](#Webpack-watch).
  14. [Webpack dev server](#Webpack-dev-server).
  15. [Webpack DevTools](#Webpack-devtools).

### 馃驴Qu茅 es Webpack?
  <h4>Ideas/conceptos claves</h4>
Module bundlers son herramientas de frontend que nos permiten usar archivos con m贸dulos JavaScript, entre otras caracter铆sticas y convertiros a un JavaScript el cual el navegador pueda entender

  <h4>Apuntes</h4> 
 Webpack es una herramienta que nos permite preparar nuestro c贸digo para llevarlo a producci贸n (module bundler)
 Webpack nos permite trabajar con:
  
  - HTML
  - CSS
  - JavaScript
  - Archivos est谩ticos
  - Im谩genes
  - Fuentes
 
  Tambien nos permite tener un modo en desarrollo para nuestros proyectos para hacer pruebas
  Nacio en el 2012, desde ese entonces varias empresas lo usan como:
  
  - Twitter
  - Instagram
  - PayPal
 
  Tambi茅n nos permite
  
  - Gestionar dependencias
  - Ejecutar tareas
  - Conversi贸n de archivos
  
  Nos permite trabajar en m贸dulos
  
  - Permiti茅ndonos tener un c贸digo separado en desarrollo, pero en producci贸n en una fuente
  - Webpack permite tener m贸dulos de JS en formato
      - AMD
      - Common JS
      - ES15
    
  RESUMEN: Webpack es un module bundler que nos permite trabajar con una variedad de tecnolog铆as web empezando desde HTML y terminando con JS. Adem谩s de tener soporte para archivos est谩ticos
  
### 馃Conseptos basicos

  **Webpack** es un paquete de m贸dulos est谩ticos para aplicaciones de JS modernas

  **Loader** Te permite hacer un bundle de cualquier recurso est谩tico m谩s all谩 de JavaScript

  **Plugins** Extienden recursos para a帽adir configuraciones y particularidades de recursos externos

<h4>Apuntes</h4>
  
- Webpack construye un gr谩fico de dependencias que mapea cada m贸dulo para con verlo en uno o m谩s m贸dulos
- Desde webpack 4 ya no dependemos de tener un archivo de configuraci贸n, pero si debemos tener un punto de entrada
- Tambien tendremos que tener un punto de salida
    - En este punto se crear谩 nuestro proyecto una vez est茅 preparado
    - Normalmente es la carpeta dist 鈬? Distribution
 
- Tambien contamos con diferentes modos
    - Modo de desarrollo
    - Modo de producci贸n
    - Modos de performance
      - Donde tu a帽ades
        - Configuraciones de minificaci贸n
        - Donde se va enviar
        - Carpeta de destino
    - Modos de desarrollo local
      - Donde puedes
        - Crear puertos espec铆ficos para tu proyecto
        - Ver cambios en tiempo real
      
- Dispone de loader y plugins permiti茅ndonos preparar particularidades de nuestro proyecto

### 馃懛鈥嶁檪锔廋reando un build con webpack

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
- La carpeta SRC es el source de todo el proyecto ( index.js , im谩genes, utils, assets, helpers, database, etc).

<h4>Instalaci贸n de Webpack</h4>

```npm
npm i webpack webpack-cli -D
```
- Y luego ejecutamos webpack npx lo que hace es ejecutar paquetes directamente de npm, este viene instalado de npm

```npm
npx webpack
```
- Al hacer esto webpack creo una carpeta llamada dist, esto lo hace por defecto webpack sin preguntarnos.

<h4>Modo de desarrollo</h4>

- Por defecto webpack al compilar nuestro proyecto setea el modo 鈥減roduction鈥? impl铆citamente pero podemos definirle el modo expl铆citamente corriendo:

```npm
npx webpack --mode production
npx webpack --mode development
```
- La diferencia radica que el modo development deja el c贸digo mas legible para los desarrolladores pero con comentarios, el modo production deja el c贸digo comprimido y mas limpio para usarse.

<h2>鈿? Configuracion de webpack.config.js</h2>
  
  - El archivo de configuraci贸n nos va ayudar a poder establecer la configuraci贸n y elementos que vamos a utilizar
  - Para poder crear el archivo de configuraci贸n en la ra铆z del proyecto creamos un archivo llamado **webpack.config.js**
  - En el mismo debemos decir
    - El punto de entrada
    - Hacia a donde a enviar la configuraci贸n de nuestro proyecto
    - Las extensiones que vamos usar 

```javascript
const path = require('path');

module.exports = {
  // Entry nos permite decir el punto de entrada de nuestra aplicaci贸n
  entry: "./src/index.js",
  // Output nos permite decir hacia d贸nde va enviar lo que va a preparar webpacks
  output: {
    // path es donde estar谩 la carpeta donde se guardar谩 los archivos
    // Con path.resolve podemos decir d贸nde va estar la carpeta y la ubicaci贸n del mismo
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

- El flag **鈥攃onfig** indica donde estar谩 nuestro archivo de configuraci贸n

```cmd
npx webpack --mode production --config webpack.config.js
```

- Para poder hacerlo m谩s amigable el comando puedes crear un script en **package.json**

```JSON
"scripts": {
		...
    "build": "webpack --mode production --config webpack.config.js"
  },
```

**RESUMEN:** Puedes crear un archivo webpack.config.js en el cual estar谩n las configuraciones con las cuales webpack trabajara, entre ellas est谩n los puntos de entrada y salida, extensiones de archivos, entre otras caracter铆sticas 

### 馃挍Babel Loader para JavaScript

 - Babel te permite hacer que tu c贸digo JavaScript sea compatible con todos los navegadores
 - Debes agregar a tu proyecto las siguientes dependencias

```npm
npm install -D babel-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime
```

- babel-loader nos permite usar babel con webpack
- @babel/core es babel en general
- @babel/preset-env trae y te permite usar las ultimas caracter铆sticas de JavaScript
- @babel/plugin-transform-runtime te permite trabajar con todo el tema de asincronismo como ser **async** y **await**
- Debes crear el archivo de configuraci贸n de babel el cual tiene como nombre **.babelrc**

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

- Para comenzar a utilizar webpack debemos agregar la siguiente configuraci贸n en **webpack.config.js**

```javascript
{
...,
module: {
    rules: [
      {
        // Test declara que extensi贸n de archivos aplicara el loader
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

**RESUMEN:** Babel te ayuda a transpilar el c贸digo JavaScript, a un resultado el cual todos los navegadores lo puedan entender y ejecutar. Trae 鈥渆xtensiones鈥? o plugins las cuales nos permiten tener caracter铆sticas m谩s all谩 del JavaScript com煤n

### 馃АHTML en Webpack

- Es un plugin que nos facilita la tarea de enlazar los bundles a nuestro template HTML

### Instalaci贸n

```npm
npm install html-webpack-plugin -D
```

- A nuestra secci贸n de webpack-config.js le agregamos la nueva configuraci贸n del plugin

```javascript
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
    mode: 'production', // LE INDICO EL MODO EXPLICITAMENTE
    entry: './src/index.js', // el punto de entrada de mi aplicaci贸n
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
        new HtmlWebpackPlugin({ // CONFIGURACI脫N DEL PLUGIN
            inject: true, // INYECTA EL BUNDLE AL TEMPLATE HTML
            template: './public/index.html', // LA RUTA AL TEMPLATE HTML
            filename: './index.html' // NOMBRE FINAL DEL ARCHIVO
        })
    ]
}
```

### 馃挋Loaders para CSS y preprocesadores de CSS

### ideas y conceptos claves
Un preprocesador CSS es un programa que te permite generar CSS a partir de la syntax 煤nica del preprocesador. Existen varios preprocesadores CSS de los cuales escoger, sin embargo, la mayor铆a de preprocesadores CSS a帽adir谩n algunas caracter铆sticas que no existen en CSS puro, como variable, mixins, selectores anidados, entre otros. Estas caracter铆sticas hacen la estructura de CSS m谩s legible y f谩cil de mantener.

post procesadores son herramientas que procesan el CSS y lo transforman en una nueva hoja de CSS que le permiten optimizar y automatizar los estilos para los navegadores actuales.

- Para dar soporte a CSS en webpack debes instalar los siguientes paquetes

```npm
npm i mini-css-extract-plugin css-loader -D
```

- css-loader 鈬? Loader para reconocer CSS
- mini-css-extract-plugin 鈬? Extrae el CSS en archivos
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

**RESUMEN:** Puedes dar soporte a CSS en webpack mediante loaders y plugins, adem谩s que puedes dar superpoderes al mismo con las nuevas herramientas conocidas como pre procesadores y post procesadores


### 馃搧Copia de archivos con webpack

- Si tienes la necesidad de mover un archivo o directorio a tu proyecto final podemos usar un plugin llamado **鈥渃opy-webpack-plugin鈥?**
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
	- From 鈬? que recurso (archivo o directorio) deseamos copiar al directorio final
	- To 鈬? en que ruta dentro de la carpeta final terminara los recursos


### 馃寙Loaders de imagenes

- Puedes usar una forma de importar las im谩genes haciendo un import de las mismas y generando una variable
- No es necesario instalar ninguna dependencia, webpack ya lo tiene incluido debemos agregar la siguiente configuraci贸n

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

- Para empezar a usar esta configuraci贸n debemos importar la imagen de la siguiente forma

```javascript
import github from '../assets/images/github.png';
```

Para incluirlo en el HTML debes hacer lo siguiente

```javascript
// Ejemplo en Vanilla JS
const imagen = `<img src=`${github}` />`;
```

### 馃敔Loaders de fuentes

- Cuando utilizamos fuentes externas una buena pr谩ctica es descargarlas a nuestro proyecto
	- Debido a que no hara un llamado a otros sitios
- Por ello es importante usarlo dentro de webpack
- Para esta tarea instalaras y usaras 鈥渇ile-loader鈥? y 鈥渦rl-loader鈥?

```NPM
npm install url-loader file-loader -D
```

- Para aplicar esta configuraci贸n debes agregar la siguiente informaci贸n

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
            // limit => limite de tama帽o
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

### 馃彈optimizaci贸n-hashes-compresi贸n-y-minificaci贸n-de-archivos

- Unos de las razones por que utilizamos webpack es porque nos permite optimizar y comprimir nuestro proyecto
- Debes utilizar los siguientes paquetes
	- css-minimizer-webpack-plugin 鈬? Nos ayuda a comprimir nuestros archivos finales CSS
	- terser-webpack-plugin 鈬? Permite minificar de una mejor forma

```NPM
npm i css-minimizer-webpack-plugin terser-webpack-plugin -D
```

- Una vez instalado el plugin debemos agregar la siguiente configuraci贸n

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

- Cuando nombremos en la configuraci贸n de webpack es importante usar [contenthash] para evitar problemas con la cache

### 馃叞Webpack Alias

- alias forma parte del objeto resolve el cual nos permite configurar la forma en que webpack resolver谩 los m贸dulos incorporados.
	- resolve.alias - para crear atajos que optimizan el tiempo de b煤squeda e incorporaci贸n de m贸dulos (commonJS o ES6)
	- resolve.extensions - para darle prioridad en resoluci贸n para con las extensiones donde si hay archivos nombrados igualmente, pero con diferentes extensiones, webpack 	resolver谩 conforme est谩n listados.
	
- Alias 鈬? nos permiten otorgar nombres paths espec铆ficos evitando los paths largos
- Para crear un alias debes agregar la siguiente configuraci贸n a webpack

```javascript
module.exports = {
	...
	resolve: {
		...
    alias: {
      '@nombreDeAlias': path.resolve(__dirname, 'src/<directorio>'),
    },
	}
}
```

- Puedes usarlo en los imports de la siguiente manera

```javasacript
import modulo from "@ejemplo/archivo.js";
```

### 馃攽Variables-de-entorno

- Es importante considerar las variables de entorno va a ser un espacio seguro donde podemos guardar datos sensibles
	- Por ejemplo, subir llaves al repositorio no es buena idea cuando tienes un proyecto open source
- Para instalar debemos correr el comando

```NPM
npm install -D dotenv-webpack
```

- Posteriormente debemos crear un archivo .env donde estar谩n la clave para acceder a la misma y el valor que contendr谩n

```
# Ejemplo
API=https://randomuser.me/api/
```

	- Es buena idea tener un archivo de ejemplo donde, el mismo si se pueda subir al repositorio como muestra de que campos van a ir

- Una vez creado el archivo .env debemos agregar la siguiente configuraci贸n en webpack.config.js

```javascript
...
const Dotenv = require('dotenv-webpack');
module.exports = {
	...
	plugins: [
		new Dotenv()
  ],
}
```

- dotenv-webpack 鈬? Leera el archivo .env por defecto y lo agregar a nuestro proyecto
- Para usarlas debes hacer lo siguiente

```javascript
const nombre = process.env.NOMBRE_VARIABLE;
```

- Toda la configuraci贸n se podr谩 acceder desde process.env

### 馃憖Webpack-watch

- El modo watch hace que nuestro proyecto se compile de forma autom谩tica
	- Es decir que est谩 atento a cambios
- Para habilitarlo debemos agregar lo siguiente en la configuraci贸n de webpack

```javascript
module.exports = {
	...
	watch: true
}
```

- Cada vez que haya un cambio hara un build autom谩tico
- Otra manera es mandar la opci贸n mediante par谩metros de consola en package.json


```json
{
	"scripts": {
		"dev:watch": "webpack --config webpack.config.dev.js --watch"
	}
}
}
```

- Vale la pena recordar que si aplicamos en modo producci贸n se tomara m谩s tiempo porque se optimizaran los recursos
	- Por ello en modo desarrollo se salta ese paso y es m谩s r谩pido la compilaci贸n


### 馃嵃Webpack-dev-server
HTML5 History API permite la manipulaci贸n de session history del navegador, es decir las p谩ginas visitadas en el tab o el frame en la cual la p谩gina est谩 cargada.

- Cuando trabajamos con webpack deseamos ver los cambios en tiempo real en un navegador
- Para tener esta caracter铆stica esta webpack-dev-server
- Para ello debemos instalarlo

```npm
npm install webpack-dev-server -D
```

- posteriormente debemos agregar la siguiente configuraci贸n en **webpack.config.dev.js**
	- Lo hacemos en la configuraci贸n de desarrollo debido a que esta caracteristica solo nos ayudara a ver cambios al momento de desarrollarla aplicaic贸n  

```javascript
mode.export ={
	...
	devServer: {
		contentBase: path.join(__dirname, 'dist'),
		compress: true,
		historyApiFallback: true,
		port: 3000,
	},
}

```

- En la configuraci贸n podemos observar las siguientes propiedades
	- **contentBass** => Le dice al servidor donde tiene que servir el contenido, solo es necesario si quieres servir archivos estaticos
	-  **compress** => Habilita la compresi贸n gzip
	-  **historyApiFallback** 鈬? cuando estas usando HTML5 History API la p谩gina index.html sera mostrada en vez de una respuesta 404
	-  **Port** 鈬? es el puerto donde vamos a realizar las peticiones
- Para comenzar a utilizarlo debes agregar el siguiente script a package.json    

```json
{
	...
	"scripts": {
	...
	"start": "webpack serve --config webpack.config.dev.js"
	}
}
```

### 馃ЗWebpack-devtools
source map es un mapeo que se realiza entre el c贸digo original y el c贸digo transformado, tanto para archivos JavaScript como para archivos CSS. De esta forma podremos debuggear tranquilamente nuestro c贸digo.

- Con las devtools de webpack te permite crear un mapa de tu proyecto y con el podemos
	- Leer a detalle
	- Analizar particularidades de lo que est谩 compilando nuestro proyecto
- Para comenzar debemos ir a webpack.config.js y agregar la propiedad devtool: "source-map"
	- Esta opci贸n genera un source map el cual posteriormente chrome lo lee y te permite depurar de una mejor forma









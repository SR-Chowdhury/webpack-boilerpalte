Webpack Boiler Plate

Getting Started: 
Webpack is an open-source JavaScript module bundler. It is made primarily for JavaScript, but it can transform front-end assets such as HTML, CSS, and images if the corresponding loaders are included.

Basic Setup
    • Let’s create a directory example: webpack-bp
    
    • Create a ‘src’ folder. Within this folder
        ◦ create a ‘scripts’ folder
            ▪ create a ‘index.js’ file
        ◦ create a ‘styles’ folder
            ▪ create a ‘index.css’ file
    • from this (webpack-bp) directory run: npm init -y
    • Create ‘webpack.config.js’ file
    • run: npm i -D webpack 
    • run: npm i -D webpack-cli
    • webpack.config.js => 
      
	const path = require('path');

	module.exports = {

		mode: 'development',
		entry: './src/scripts/index.js',
		output: {
			path: path.resolve(__dirname, 'dist'),
			filename: 'bundle.js',
		},

	};

    • package.json =>
      
      "scripts": {
		"build": "webpack",
	},

    • index.html =>
      
      <!DOCTYPE html>
	<html lang="en">
	<head>
		<meta charset="UTF-8">
		<meta http-equiv="X-UA-Compatible" content="IE=edge">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>Webpack Boiler Plate</title>
	</head>
	<body>
		<h1>Bismillahir Rahmanir Rahim</h1>

	<script src="/dist/bundle.js"></script>
	</body>
	</html>

    • index.js
      
      const fun = () => console.log('Allahuakbar');
	fun();

    • You are now ready to show output [npm run build]
    
Now time is coming for using bable-loader for converting ES6 to ES5

run: 
	npm install i -D babel-loader @babel/core @babel/preset-env webpack
	
run:
	npm install i -D@babel/plugin-proposal-class-properties


Update ‘webpack.config.js’ =>

	module: {
		rules: 
		[
			// Babel Loader with plugins
			{
				test: /\.m?js$/,
				exclude: /(node_modules|bower_components)/,
				use: {
					loader: 'babel-loader',
					options: {
						presets: ['@babel/preset-env'],
						plugins: ['@babel/plugin-proposal-class-properties']
					}
				}
			},
		]
	},
	
	
Now we are using CSS loader with MiniCssExtractPlugin

run: 

	npm install --save-dev css-loader mini-css-extract-plugin
	
Update index.html =>

	<link rel="stylesheet" href="/dist/main.css">

Update webpack.config.js =>

	const MiniCssExtractPlugin = require('mini-css-extract-plugin');

Inside module.exports  add =>

	// CSS Loader
	{
		test: /\.css$/,
		use: [
			MiniCssExtractPlugin.loader, // instead of "style-loader",
	'		css-loader'
		],
	},

	plugins: [
		new MiniCssExtractPlugin({
			filename: '[name].css',
			chunkFilename: '[id].css',
		}),
	]

Update index.js =>

	import '../styles/index.css';


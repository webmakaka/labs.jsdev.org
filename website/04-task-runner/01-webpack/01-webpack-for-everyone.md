---
layout: page
title: Webpack for Everyone [ENG, 2017]
description: Webpack for Everyone
keywords: Webpack for Everyone
permalink: /tasks-runner/webpack/webpack-for-everyone/
---

# [Laracasts.com] Webpack for Everyone [ENG, 2017]

<br/>
<br/>

**Looks like that video for free:**  
https://laracasts.com/series/webpack-for-everyone

MySRC (many branches):  
https://bitbucket.org/marley-nodejs/webpack-for-everyone/

<br/>

### Prepare Environment

<br/>

    $ mkdir -p /projects/js/webpack/webpack-for-everyone/

<br/>

    $ docker run -it \
    -p 80:8080 -p 1337:1337 -p 3000:3000 -p 4000:4000 -p 5000:5000 -p 6000:6000 -p 7000:7000 -p 8000:8000 -p 9000:9000 \
    --name webpack-for-everyone \
    -v /projects/js/webpack/webpack-for-everyone/:/project \
    node \
    /bin/bash

<br/>

    # apt-get update
    # apt-get install -y vim git

<br/>

### 01-Zero-Config-Webpack-Compilation

    # cd /project
    # npm init -y

    $ npm i -g webpack


    -- ("webpack": "^2.6.1")
    # npm install --save-dev webpack


    # mkdir -p src
    # vi src/main.js

<br/>

    alert('main');

<br/>

    # vi index.html

<br/>

    <html>
        <head>
            <title></title>
        </head>


    <body>

        <h1>Hello World!</h1>


        <script src="dist/bundle.js"></script>

    </body>


    </html>

<br/>

    # vi package.json

    "scripts": {
        "build": "webpack src/main.js dist/bundle.js",
        "watch": "npm run build -- --watch"
      },

<br/>

     # npm run build
     # npm run watch

<br/>

### 02-A-Dedicated-Configuration-File

    # vi webpack.config.js

<br/>

    var webpack = require('webpack');
    const path = require('path');

    module.exports = {

        entry: './src/main.js',
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'bundle.js'
        }

    };

<br/>

    # vi package.json

    "scripts": {
        "build": "webpack",
        "watch": "npm run build -- --watch"
      },

<br/>

    # npm run build
    # npm run watch

<br/>

### 03-Modules-Are-Just-Files

<br/>

    # vi src/main.js

<br/>

    import notification from './Notification';

    notification.log('here we go');
    notification.announce('here we go as an alert');

<br/><br/>

    # vi src/Notification.js

<br/>

    function announce (message) {
        alert(message);
    }

    function log (message) {
        console.log(message);
    }

    export default {
        announce: announce,
        log: log
    };

<br/><br/>

    # npm run watch

<br/>

### 04-Loaders-Are-Transformers

<br/>

    # npm install --save-dev css-loader
    # npm install --save-dev style-loader

<br/>

    # vi src/main.js

<br/>

    require('./main.css');

<br/>

    # vi src/main.css

<br/>

    # vi src/main.css

<br/>

    body {
        background: red;
    }

<br/>

    # vi webpack.config.js

<br/>

    var webpack = require('webpack');
    const path = require('path');

    module.exports = {

        entry: './src/main.js',
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'bundle.js'
        },

        module: {
            rules: [
                {
                    test: /\.css$/,
                    use: ['style-loader', 'css-loader']
                }
            ]
        }
    };

<br/>

    # npm run build

<br/>

### 05-ES2015-Compilation-With-Babel

http://babeljs.io/docs/setup/#installation

    # npm install --save-dev babel-loader babel-core

http://babeljs.io/docs/plugins/

    # npm install --save-dev babel-cli babel-preset-es2015

<br/>

    # echo '{ "presets": ["es2015"] }' > .babelrc

<br/>

    # vi src/main.js

<br/>

    class Form {
        constructor(){
            alert('Yay Form classes are great no matter what JS developers say!');

            let numbers = [5, 10, 15].map(number => number * 2);

            console.log(numbers);
        }
    }


    new Form();

<br/>

    # vi webpack.config.js

<br/>

    var webpack = require('webpack');
    const path = require('path');

    module.exports = {

        entry: './src/main.js',
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'bundle.js'
        },

        module: {
            rules: [
                {
                    test: /\.css$/,
                    use: ['style-loader', 'css-loader']
                },

                {
                    test: /\.js$/,
                    exclude: /node_modules/,
                    loader: "babel-loader" }
            ]
        }
    };

<br/>

    # npm run build

<br/>

### 06-Minification-and-Environments

<br/>

    # vi webpack.config.js

<br/>

    var webpack = require('webpack');
    const path = require('path');

    var inProduction = (process.env.NODE_ENV === 'production');

    module.exports = {

        entry: './src/main.js',
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'bundle.js'
        },

        module: {
            rules: [
                {
                    test: /\.css$/,
                    use: ['style-loader', 'css-loader']
                },

                {
                    test: /\.js$/,
                    exclude: /node_modules/,
                    loader: "babel-loader" }
            ]
        },

        plugins: [


        ]
    };

    if (inProduction){
        module.exports.plugins.push(
            new webpack.optimize.UglifyJsPlugin()
        );
    }

<br/>

    # vi package.json

<br/>

    "scripts": {
        "dev": "webpack",
        "prod": "NODE_ENV=production webpack",
        "watch": "npm run build -- --watch"
    },

<br/>

    # npm run dev
    # npm run prod

<br/>

### 07-Sass-Compilation

    # npm install --save-dev sass-loader node-sass

<br/>

    # vi src/main.js

<br/>

    require('./main.scss');

<br/>

    # vi src/main.scss

<br/>

    $primary: green;

    body {
        background: $primary;
    }

<br/>

    # vi webpack.config.js

<br/>

    var webpack = require('webpack');
    const path = require('path');

    var inProduction = (process.env.NODE_ENV === 'production');

    module.exports = {

    entry: './src/main.js',
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'bundle.js'
    },

    module: {
        rules: [
            {
                test: /\.s[ac]ss$/,
                use: ['style-loader', 'css-loader', 'sass-loader']
            },

            {
                test: /\.css$/,
                use: ['style-loader', 'css-loader']
            },

            {
                test: /\.js$/,
                exclude: /node_modules/,
                loader: "babel-loader" }
        ]
    },

    plugins: [


    ]
    };

    if (inProduction){
        module.exports.plugins.push(
            new webpack.optimize.UglifyJsPlugin()
        );
    }

<br/>

    # npm run dev

<br/>

### 08-Extract-CSS-To-A-Dedicated-File

https://github.com/webpack-contrib/extract-text-webpack-plugin

    # npm install --save-dev extract-text-webpack-plugin

https://webpack.js.org/plugins/loader-options-plugin/

<br/>

    # vi src/main.js

<br/>

    alert('empty');

<br/>

    # vi webpack.config.js

<br/>

    var webpack = require('webpack');
    const path = require('path');

    const ExtractTextPlugin = require("extract-text-webpack-plugin");

    var inProduction = (process.env.NODE_ENV === 'production');

    module.exports = {

        entry: {
            app: ['./src/main.js',
                 './src/main.scss']
        },
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: '[name].js'
        },

        module: {
            rules: [
                {
                    test: /\.s[ac]ss$/,
                    use: ExtractTextPlugin.extract({
                        use: ['css-loader', 'sass-loader'],
                        fallback: 'style-loader'
                    })
                },


                {
                    test: /\.js$/,
                    exclude: /node_modules/,
                    loader: "babel-loader" }
            ]
        },

        plugins: [
            new ExtractTextPlugin('[name].css'),

            new webpack.LoaderOptionsPlugin({
                  minimize: inProduction
                })

        ]
    };

    if (inProduction){
        module.exports.plugins.push(
            new webpack.optimize.UglifyJsPlugin()
        );
    }

<br/>

    # npm run dev
    # npm run prod

<br/>

### 09-The-Relative-CSS-Url-Conundrum

https://github.com/webpack-contrib/css-loader

<br/>

    # npm install --save-dev file-loader

<br/>

    # vi src/main.scss

<br/>

    .test {
        background: url('./images/cat.jpg');
    }

<br/>

    # vi webpack.config.js

<br/>

    var webpack = require('webpack');
    const path = require('path');

    const ExtractTextPlugin = require("extract-text-webpack-plugin");

    var inProduction = (process.env.NODE_ENV === 'production');

    module.exports = {

        entry: {
            app: ['./src/main.js',
                 './src/main.scss']
        },
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: '[name].js'
        },

        module: {
            rules: [
                {
                    test: /\.s[ac]ss$/,
                    use: ExtractTextPlugin.extract({
                        use: ['css-loader', 'sass-loader'],
                        fallback: 'style-loader'
                    })
                },

                {
                    test: /\.(png|jpe?g|gif|svg|eot|ttf|woff|woff2)$/,
                    loader: 'file-loader',
                    options: {
                        name: 'images/[name].[hash].[ext]'
                    }
                },

                {
                    test: /\.js$/,
                    exclude: /node_modules/,
                    loader: "babel-loader" }
            ]
        },

        plugins: [
            new ExtractTextPlugin('[name].css'),

            new webpack.LoaderOptionsPlugin({
                  minimize: inProduction
                })

        ]
    };

    if (inProduction){
        module.exports.plugins.push(
            new webpack.optimize.UglifyJsPlugin()
        );
    }

<br/>

    # npm run dev

<br/>

### 10-Strip-Unused-CSS-Automatically

https://github.com/webpack-contrib/purifycss-webpack

<br/>

    # npm i -D purifycss-webpack purify-css

<br/>

    # vi index.html

<br/>

    <html>
        <head>
            <title></title>
        </head>


    <body>

        <h1>Hello World!</h1>

        <div class="two">Hello</div>


        <script src="dist/bundle.js"></script>

    </body>


    </html>

<br/>

    # vi src/main.scss

<br/>

    .one {
        background: red;
    }

    .two {
        background: green;
    }

<br/>

    # vi webpack.config.js

<br/>

    var webpack = require('webpack');
    const path = require('path');
    const glob = require('glob');

    const ExtractTextPlugin = require("extract-text-webpack-plugin");
    const PurifyCSSPlugin = require('purifycss-webpack');

    var inProduction = (process.env.NODE_ENV === 'production');

    module.exports = {

        entry: {
            app: ['./src/main.js',
                 './src/main.scss']
        },
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: '[name].js'
        },

        module: {
            rules: [
                {
                    test: /\.s[ac]ss$/,
                    use: ExtractTextPlugin.extract({
                        use: ['css-loader', 'sass-loader'],
                        fallback: 'style-loader'
                    })
                },

                {
                    test: /\.(png|jpe?g|gif|svg|eot|ttf|woff|woff2)$/,
                    loader: 'file-loader',
                    options: {
                        name: 'images/[name].[hash].[ext]'
                    }
                },

                {
                    test: /\.js$/,
                    exclude: /node_modules/,
                    loader: "babel-loader" }
            ]
        },

        plugins: [
            new ExtractTextPlugin('[name].css'),

            new PurifyCSSPlugin({
             // paths: glob.sync(path.join(__dirname, 'app/*.html')),
             paths: glob.sync(path.join(__dirname, 'index.html')),

             minimize: inProduction

            }),

            new webpack.LoaderOptionsPlugin({
                  minimize: inProduction
            })

        ]
    };

    if (inProduction){
        module.exports.plugins.push(
            new webpack.optimize.UglifyJsPlugin()
        );
    }

<br/>

    # npm run dev

<br/>

### 11-File-Hashing

    # npm install jquery -D

https://github.com/johnagan/clean-webpack-plugin

    # npm install --save-dev clean-webpack-plugin

<br/>

    # vi webpack.config.js

<br/>

    var webpack = require('webpack');
    const path = require('path');
    const glob = require('glob');

    const ExtractTextPlugin = require("extract-text-webpack-plugin");
    const PurifyCSSPlugin = require('purifycss-webpack');
    const CleanWebpackPlugin = require('clean-webpack-plugin');

    var inProduction = (process.env.NODE_ENV === 'production');

    module.exports = {

        entry: {
            app: ['./src/main.js',
                 './src/main.scss'],
            vendor: ['jquery']
        },
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: '[name].[chunkhash].js'
        },

        module: {
            rules: [
                {
                    test: /\.s[ac]ss$/,
                    use: ExtractTextPlugin.extract({
                        use: ['css-loader', 'sass-loader'],
                        fallback: 'style-loader'
                    })
                },

                {
                    test: /\.(png|jpe?g|gif|svg|eot|ttf|woff|woff2)$/,
                    loader: 'file-loader',
                    options: {
                        name: 'images/[name].[hash].[ext]'
                    }
                },

                {
                    test: /\.js$/,
                    exclude: /node_modules/,
                    loader: "babel-loader" }
            ]
        },

        plugins: [

            new CleanWebpackPlugin(['dist']),

            new ExtractTextPlugin('[name].css'),

            new PurifyCSSPlugin({
             // paths: glob.sync(path.join(__dirname, 'app/*.html')),
             paths: glob.sync(path.join(__dirname, 'index.html')),

             minimize: inProduction

            }),

            new webpack.LoaderOptionsPlugin({
                  minimize: inProduction
            })

        ]
    };

    if (inProduction){
        module.exports.plugins.push(
            new webpack.optimize.UglifyJsPlugin()
        );
    }

<br/>

    # npm run dev

<br/>

### 12-Webpack-Manifests

<br/>

    # vi webpack.config.js

<br/>

    var webpack = require('webpack');
    const path = require('path');
    const glob = require('glob');

    const ExtractTextPlugin = require("extract-text-webpack-plugin");
    const PurifyCSSPlugin = require('purifycss-webpack');
    const CleanWebpackPlugin = require('clean-webpack-plugin');

    var inProduction = (process.env.NODE_ENV === 'production');

    module.exports = {

        entry: {
            app: ['./src/main.js',
                 './src/main.scss'],
            vendor: ['jquery']
        },
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: '[name].[chunkhash].js'
        },

        module: {
            rules: [
                {
                    test: /\.s[ac]ss$/,
                    use: ExtractTextPlugin.extract({
                        use: ['css-loader', 'sass-loader'],
                        fallback: 'style-loader'
                    })
                },

                {
                    test: /\.(png|jpe?g|gif|svg|eot|ttf|woff|woff2)$/,
                    loader: 'file-loader',
                    options: {
                        name: 'images/[name].[hash].[ext]'
                    }
                },

                {
                    test: /\.js$/,
                    exclude: /node_modules/,
                    loader: "babel-loader" }
            ]
        },

        plugins: [

            new CleanWebpackPlugin(['dist']),

            new ExtractTextPlugin('[name].css'),

            new PurifyCSSPlugin({
             // paths: glob.sync(path.join(__dirname, 'app/*.html')),
             paths: glob.sync(path.join(__dirname, 'index.html')),

             minimize: inProduction

            }),

            new webpack.LoaderOptionsPlugin({
                  minimize: inProduction
            }),

            function(){
                this.plugin('done', stats => {
                    require('fs').writeFileSync(
                        path.join(__dirname, 'dist/mainfest.json'),
                        JSON.stringify(stats.toJson().assetsByChunkName)
                    );
                });
            }

        ]
    };

    if (inProduction){
        module.exports.plugins.push(
            new webpack.optimize.UglifyJsPlugin()
        );
    }

<br/>

    # npm run dev

<br/>

### 13-Automatic-Image-Optimization

https://github.com/thetalecrafter/img-loader

    # npm install --save-dev img-loader

<br/>

<br/>

    # vi webpack.config.js

<br/>

    var webpack = require('webpack');
    const path = require('path');
    const glob = require('glob');

    const ExtractTextPlugin = require("extract-text-webpack-plugin");
    const PurifyCSSPlugin = require('purifycss-webpack');
    const CleanWebpackPlugin = require('clean-webpack-plugin');

    var inProduction = (process.env.NODE_ENV === 'production');

    module.exports = {

        entry: {
            app: ['./src/main.js',
                 './src/main.scss'],
            vendor: ['jquery']
        },
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: '[name].[chunkhash].js'
        },

        module: {
            rules: [

                {
                    test: /\.css$/,
                    use: 'css-loader'
                },

                {
                    test: /\.s[ac]ss$/,
                    use: ExtractTextPlugin.extract({
                        use: ['css-loader', 'sass-loader'],
                        fallback: 'style-loader'
                    })
                },

                {
                    test: /\.(png|jpe?g|gif|svg|eot|ttf|woff|woff2)$/,

                    loaders: [
                        {
                            loader: 'file-loader',
                            options: {
                                name: 'images/[name].[hash].[ext]'
                            }
                        },

                        'img-loader'
                    ]

                },

                {
                    test: /\.js$/,
                    exclude: /node_modules/,
                    loader: "babel-loader" }
            ]
        },

        plugins: [

            new CleanWebpackPlugin(['dist']),

            new ExtractTextPlugin('[name].css'),

            new PurifyCSSPlugin({
             // paths: glob.sync(path.join(__dirname, 'app/*.html')),
             paths: glob.sync(path.join(__dirname, 'index.html')),

             minimize: inProduction

            }),

            new webpack.LoaderOptionsPlugin({
                  minimize: inProduction
            }),

            function(){
                this.plugin('done', stats => {
                    require('fs').writeFileSync(
                        path.join(__dirname, 'dist/mainfest.json'),
                        JSON.stringify(stats.toJson().assetsByChunkName)
                    );
                });
            }

        ]
    };

    if (inProduction){
        module.exports.plugins.push(
            new webpack.optimize.UglifyJsPlugin()
        );
    }

<br/>

    # npm run dev

<br/>

### 14-Developing-Webpack-Plugins

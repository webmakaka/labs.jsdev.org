---
layout: page
title: WebPack - Applying Webpack to a Real Project
permalink: /tasks-runner/webpack/webpack-2-the-complete-developers-guide/applying- webpack-to-a-real-project/
---

<br/>

# WebPack - Applying Webpack to a Real Project

<br/>

### A Real World Project

src:  
https://github.com/StephenGrider/WebpackProject

    $ git clone https://github.com/StephenGrider/WebpackProject.git

    # cd WebpackProject/
    # npm install

<br/>    
    
### Setting Up Babel

    webpack.config.js

<br/>

    module: {
    rules: [
        {
            use: 'babel-loader',
            test: /\.js$/,
            exclude: /node_modules/
        },
        {
            use: ['style-loader', 'css-loader'],
            test: /\.css$/
        }
    ]
    }

<br/>    
    
### Minimum Webpack Config

    .babelrc

<br/>

    {
        "presets": ["babel-preset-env", "react"]
    }

<br/>

    # npm run build

<br/>

### Vendor Asset Caching

<br/>

<div align="center">
    <img src="/img/webpack/vendor-asset-caching-01.png" alt="Vendor Asset Caching">
</div>

<br/>

<div align="center">
    <img src="/img/webpack/vendor-asset-caching-02.png" alt="Vendor Asset Caching">
</div>

<br/>

<div align="center">
    <img src="/img/webpack/vendor-asset-caching-03.png" alt="Vendor Asset Caching">
</div>

<br/>

### Refactoring for Vendor Splitting

    webpack.config.js

<br/>

    const VENDOR_LIBS = [
        'faker',
        'lodash',
        'react',
        'react-dom',
        'react-input-range',
        'react-redux',
        'react-router',
        'redux',
        'redux-form',
        'redux-thunk'
    ];

    module.exports = {
      entry: {
          bundle: './src/index.js',
          vendor: VENDOR_LIBS
      },
      output: {
        path: path.join(__dirname, 'dist'),
        filename: '[name].js'
    },

<br/>

    # npm run build

<br/>

### Effect of Code Splitting

<br/>

<div align="center">
    <img src="/img/webpack/effect-of-code-splitting-01.png" alt="Effect of Code Splitting">
</div>

<br/>

    webpack.config.js

<br/>

    plugins: [
        new webpack.optimize.CommonsChunkPlugin({
            name: 'vendor'
        })
    ]

<br/>

### Troubleshooting Vendor Bundles

    # npm install --save-dev html-webpack-plugin

<br/>

        webpack.config.js

<br/>
    
    ***
    
    var HtmlWebpackPlugin = require('html-webpack-plugin');
    
    ***

    new HtmlWebpackPlugin({
        template: 'src/index.html'
    })

<br/>

### Chunk Hashing for Cache Busting

<br/>

        webpack.config.js

<br/>

    ***

    filename: '[name].[chunkhash].js'

    ***

    names: ['vendor', 'manifest']

<br/>

### Cleaning Project Files

    # npm install --save-dev rimraf

<br/>

    package.json

<br/>

    "scripts": {
      "clean": "rimraf dist",
      "build": "npm run clean && webpack"
    },

<br/>

    # npm run build

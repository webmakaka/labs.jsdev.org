---
layout: page
title: WebPack - Building for Performance with Webpack
permalink: /tasks-runner/webpack/webpack-2-the-complete-developers-guide/building-for-performance-with-webpack/
---

<br/>

# WebPack - Building for Performance with Webpack

<br/>

<div align="center">
    <img src="/img/webpack/building-for-performance-with-webpack-01.png" alt="building for performance with webpack">
</div>

<br/><br/>

<div align="center">
    <img src="/img/webpack/building-for-performance-with-webpack-02.png" alt="building for performance with webpack">
</div>

<br/><br/>

<div align="center">
    <img src="/img/webpack/building-for-performance-with-webpack-03.png" alt="building for performance with webpack">
</div>

<br/><br/>

<div align="center">
    <img src="/img/webpack/building-for-performance-with-webpack-04.png" alt="building for performance with webpack">
</div>

<br/><br/>

<div align="center">
    <img src="/img/webpack/building-for-performance-with-webpack-05.png" alt="building for performance with webpack">
</div>

<br/><br/>

<div align="center">
    <img src="/img/webpack/building-for-performance-with-webpack-07.png" alt="building for performance with webpack">
</div>

<br/><br/>

<div align="center">
    <img src="/img/webpack/building-for-performance-with-webpack-08.png" alt="building for performance with webpack">
</div>

<br/><br/>

    # vi src/index.js

<br/>

    const button = document.createElement('button');
    button.innerText = 'Click me';
    button.onclick = () => {
        System.import('./image_viewer').then(module => {
            // console.log(module);
            module.default();
        });
    };

    document.body.appendChild(button);

<br/>

    # vi src/image_viewer.js

<br/>

    import small from '../assets/small.jpg';
    import '../styles/image_viewer.css';

    export default () => {
        const image = document.createElement('img');
        image.src = small;

        document.body.appendChild(image);
    };

<br/>

    # npm run build

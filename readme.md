# **CPSC 5416**: Content- Aware Image Resizing by Seam Carving on Javascript

### Group Member
1. [Wang, Pengyu](https://github.com/PengyuW007), 0425157
2. [Zhang, Haokun](https://github.com/haokunzhang), 0424660
3. [Zhu, Ziping](https://github.com/0v0-QAQ), 0422426

### Description
Javascript implementation of a content-aware image resizing algorithm called seam carving. <a href="https://en.wikipedia.org/wiki/Seam_carving">Seam carving</a> 
crops an image by removing the "least important" pixels in an image. 
An "unimportant" pixel is defined as a pixel which is very similar to its surrounding pixels. 
A seam is a one pixel column in the image which can zig-zag between adjacent columns. 
We use [Seam Carving System](https://github.com/mfbx9da4/seam-carving-js) as the prototype, then we added some new features to make it clearer to show the process.

![image](https://user-images.githubusercontent.com/1690659/64417276-b1e5b480-d090-11e9-82ac-c3cfd79b9a85.png)

![image](https://user-images.githubusercontent.com/1690659/64417322-c2962a80-d090-11e9-8415-ffec76231ea1.png)

### [Repository](https://github.com/haokunzhang/seam-carving-js)

### [Presentation](https://docs.google.com/presentation/d/1baefUtgnmUMQzuKE2jryYe5W-C1SlbvDpIwdUpSS4Gk/edit#slide=id.p)

### Documents
1. [CPSC 5416 Content-Aware Image Resizing by Seam Carving](https://github.com/haokunzhang/seam-carving-js/blob/master/CPSC_5416%20Content-Aware%20Image%20Resizing%20by%20Seam%20Caving.pdf)
2. [Google Doc Paper, (need access)](https://docs.google.com/document/d/1Ui7vCC1XvcsmRQbe1Od_U7_W2YEoPmc7rzNO8YZXfNg/edit)
3. [Shai Avidan and Ariel Shamir's Algorithm](https://perso.crans.org/frenoy/matlab2012/seamcarving.pdf)

## Compile and Run
    click index.html to run

## Install

    npm install seam-carving-js

## Install for contributors

OSX requires

    brew install pkg-config cairo libpng jpeg giflib
    xcode-select --install # el capitain only

Ubuntu

    sudo apt-get install libcairo2-dev libjpeg8-dev libpango1.0-dev libgif-dev build-essential g++

Everyone

    npm install

## Build

    gulp build
    
## Test

    npm run test

## Run demo

    npm install -g local-web-server
    ws # navigate to http://localhost:63342

## Current optimizations
- When we remove a seam not all pixels are recalculated instead only pixels either side of the seam are enqueued to be recalculated. If the min sum of the affected pixel has not changed we need not enqueue it's children.

## Potential optimizations

- Move SeamCarver to web worker
- Iterate arrays in a CPU cache efficient way
- Keep track of smallest on top row
- Have three matrices, one for minx, one for vminsum and one for energies so that we can use typed arrays
- Could convert picture rgba array to [`Uint32Array` rgb number array](https://hacks.mozilla.org/2011/12/faster-canvas-pixel-manipulation-with-typed-arrays/) to save space
- Do logical deletes on the energy matrix. This way the cost of deletion goes way down, with the cost of finding the neighbor when recalculating going up some. Would have to keep picture array as an array of `Uint8ClampedArray`s.
- Potentially could add the pixels which we need to recalculate the energy for to a queue of nodes and relax there edges to adjacent pixels. If we do not find a smaller vminsum for any pixel on the queue we do not need to iterate its descendants.
- There might be a (slightly) better way to remove the seam, with less conversion between coordinates.

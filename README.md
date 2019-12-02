# lfcam

This is the source code for the light field image manipulator demo available here: https://lfcam.nrempel.com.

## Caveats

The code is a bit of a mess due to time contraints. Additionally, this demo uses overlapping divs with css opacity. This would be much more efficient if it used a single canvas element.

The image offset can be calibrated in x and y direction, but refocusing an image only occurs on the x-axis right now so try to take your photographs in a relatively horizontal line.

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

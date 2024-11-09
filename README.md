# How to Configure SASS for React Applications

Hint: use vite app if you're using SASS for styling. Reason ---> easy to configure

<br />

## A) If we're using standard CRA project

In a standard Create React App (CRA) project, you don’t have direct access to the build configuration like you do with Vite. There're two way to configure the CRA configurations.

1. Eject CRA and update Webpack manually
2. Override Webpack configurations by using 3rd party tool like `@craco/craco`

### Method 01: Manual WebPack Configuration

```sh
# Step 01
npm install sass react-scripts@latest

# Step 02
npm run eject
```

**Then Update Webpack as follows**

After ejecting, you’ll find Webpack configuration files in the `config` folder:

`config/webpack.config.js`: Main Webpack configuration file.

```sh
npm install sass-loader@latest
```

Update Webpack Config to Use Dart Sass’s New API: Open `config/webpack.config.js`. In this file, locate the rules for handling SCSS files. The relevant section usually looks like this (it may be within an array under `oneOf`):

```js
{
  test: /\.(scss|sass)$/,
  use: [
    require.resolve('style-loader'),
    {
      loader: require.resolve('css-loader'),
      options: {
        importLoaders: 2,
        sourceMap: isEnvProduction && shouldUseSourceMap,
      },
    },
    {
      loader: require.resolve('sass-loader'),
      options: {
        sourceMap: isEnvProduction && shouldUseSourceMap,
        // Add the following line to specify the use of Dart Sass
        implementation: require('sass'),
      },
    },
  ],
}
```

<br />

## B) If we're using vite project

```sh
# Create vite app
npm create vite@latest my-app
```

Configure the vite.config file as follows

```js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

// https://vite.dev/config/
export default defineConfig({
  plugins: [react()],
  css: {
    preprocessorOptions: {
      scss: {
        api: "modern-compiler",
      },
    },
  },
});
```

```js
// SASS Configurations
css: {
    preprocessorOptions: {
      scss: {
        api: "modern-compiler",
      },
    },
  },
```

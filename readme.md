#Webpack Notes

* Webpack is a module bundler->Main purpose of webpack is to  create a single file to be fetched to browser

* There are many different things we can do with webpack,using of loaders of webpack we can perform various actios 
of different kind of files.




#####Build
`npm install -g webpack`


####Run
We can directly run webpack from  terminal without the need of `webpack.config.js` file.
`webpack 'srcfile' 'distfile'`

[using webpack form cli](https://github.com/webpack/docs/wiki/cli)


#####Using with react

1. To compile react (jsx) we will have to use some loaders and presets
    ```
        npm install babel-core babel-loader --save-dev
        npm install babel-preset-es2015 --save-dev
        npm install babel-preset-react --save-dev
    ```

    Webpack treats every file (.css,.html,..) as different module,and it only understands javascript,so 
     loaders transforms these modules.
1. To use babel a `.babelrc` file needs to be created.
a .babelrc file looks like this 



```
        {
          "presets": [
            "es2015",
            "react"
          ],
      
        }
```

babel can do nothing on its own,it uses various plugins and presets(a collections of plugins)


1. use `webpack --module-bind='js=babel-loader' ./src/js/main.js ./dist/bundel.js` to run webpack.
here **js=babel-loader** just tells webpack to run all js files through babel-loader.
*it is advisable to not use all plugins in production env,as they could increase the  productoin build size* 


######Webpackpack.config.js
Alternatively we can create a config file.

sample file

```
module.exports={
    entry:'./src/js/main.js',
    output:{
        filename:'./dist/bundle.js'
    },
    devtool:'eval',


  watch:true,
  module: {
     loaders: [
       {
         test: /\.js$/,
         exclude: /node_modules/,
         loader: 'babel-loader',
         query: {
           presets: ['react', 'es2015']
         }
       }
     ]
 },
 resolve: {
   extensions: ['.js', '.es6']
 }
}

```


here
* **Entry/outfile** are paths of entry and output files
* **devtool** is mainly used for debugging purpose,otherwise webpack displays all log messages inside refering to bundle,which is really pain while debugging
* **module** contains list of all the loaders which will be executed if regex (`test`) for file name pases,  








# Module Bundler
![](https://i.imgur.com/tPPsDbS.png)

## Webpack

### Install
Install in develop environment
```javascript=
npm install --save-dev webpack webpack-dev-server webpack-cli

// �w�� babel ������ module
// babel-core: Babel ���D�n�{��
// babel-loader: �� webpack ����ϥ� Babel
// babel-preset-env: �N ES6+ ���y�k��Ķ�� ES5
// babel-preset-react: �sĶ JSX
npm install --save-dev babel-core babel-loader babel-preset-env babel-preset-react

// �w�� eslint ������ module
// eslint: �D�{��
// eslint-loader: �� webpack �ϥ� eslint
// babel-eslint: �� eslint ������ܨ�|���䴩���y�k���~
npm install --save-dev eslint eslint-loader babel-eslint

// �ϥ� eslint-config-airbnb ���W�h�ݭn�w�˥H�U modules
npm install --save-dev eslint-config-airbnb eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react

```

### Setup
`package.json` �s�W `start` script
```javascript=
  "scripts": {
    "start": "webpack-dev-server --config ./webpack.config.js --mode development"
  }
```

`.babelrc` �]�w babel ������ config
```json=
{
    "presets": [
        "env",
        "react"
    ]
}
```

`.eslintrc` �]�w eslint ������ config
```json=
{
    "parser": "babel-eslint",
    "rules": {
        // �p�G�{������ console �h�|���� warning
        "no-console": "warn"
    },
    // �ϥ� eslint-config-airbnb ���W�h�ݭn�W�[�U�� extends �]�w
    "extends": [        
        "airbnb"
    ]
}
```

`webpack.config.js`
* entry: ���ѵ{�����i�J�I�� webpack
* output: bundle ���ɮצs���m���ɦW
* module: ���� rules �Ψӳ]�w�h�ӳW�h�A�� webpack ����ɦW(�z�Ltest�ݩ�)�A�èϥΥ��T��loader
* resolve: import �ɮ׮ɡA�p�G���ɦW�O resolve ���]�w���h�i�H�ٲ�
* devServer: �]�w�n�� server ���ѪA�Ȫ����|
```javascript=
module.exports = {    
    entry: [
        './src/index.js'
    ],
    output: {
        path: __dirname + '/dist',
        publicPath: '/',
        filename: 'bundle.js'
    },    
    module: {
        rules: [
            {
                test: /\.(js|jsx)/,
                exclude: /node_modules/,
                use: ['babel-loader']
            },
            {
                test: /\.(js|jsx)/,
                exclude: /node_modules/,
                use: ['eslint-loader']
            }
        ]
    },
    resolve: {
        extensions: ['.js', '.jsx']
    },
    devServer: {
        contentBase: './dist'
    }
}
```

[online webpack confing creator](https://webpack.jakoblind.no/)


## Parcel

### Install
```javascript=
npm install --save-dev parcel-bundler babel-preset-env babel-preset-react
```

### Setup
* ���ϥΨ� Babel �@�˭n�]�m `.babelrc`
* �b`package.json`���]�w `start` script
```javascript=
"scripts": {
    "start": "parcel index.html"
},
```

### Usage
���� `npm start` �AParcel �|�q `index.html` ���i�J�I�}�l�ѪR�A���󦳥Ψ쪺JS�BCSS�BIMAGE�������|���]����

### Refference
[�x��](https://parceljs.org/)
[�������](http://www.css88.com/doc/parcel/getting_started.html)
# NextJS + Typescript + Prettier + Eslint + Sass + Tailwind + [VSCode Settings]

Exemplo de setup para começar um projeto no VSCode utilizando:

- NextJS;
- Typescript
- Prettier;
- Eslint;
- Sass;
- Tailwind;
- PostCSS;
- Stylelint
- Editorconfig
- .env

## Utilizando Tailwind/ Sass com NextJS

### Instalando SASS
```
npm install sass

ou

yarn add sass
```

### Instalando o Tailwind, PostCSS e dependências
```
npm install tailwindcss postcss-flexbugs-fixes postcss-preset-env postcss-import precss -D

ou

yarn add tailwindcss postcss-flexbugs-fixes postcss-preset-env postcss-import precss --save-dev
```

### Configurando o PostCSS
Crie o arquivo *postcss.config.js* e deixe-o assim:

```
module.exports = {
  plugins: {
    'postcss-import': {},
    autoprefixer: {},
    tailwindcss: {},
    'postcss-flexbugs-fixes': {},
    'postcss-preset-env': {
      autoprefixer: {
        flexbox: 'no-2009'
      },
      stage: 3,
      features: {
        'custom-properties': false
      }
    }
  }
};
```

### Confirgurando o NextJS
Crie o arquivo *next.config.js* e deixe-o assim:

```
const path = require('path');

module.exports = {
  trailingSlash: false,
  webpackDevMiddleware: (config) => {
    config.watchOptions = {
      poll: 1000,
      aggregateTimeout: 300
    };

    return config;
  },
  sassOptions: {
    includePaths: [path.join(__dirname, 'styles')]
  }
};
```

### Configurando o Tailwind
Crie o arquivo *tailwind.config.js* e deixe-o assim:

```
module.exports = {
  // @see https://tailwindcss.com/docs/upcoming-changes
  future: {
    removeDeprecatedGapUtilities: true,
    purgeLayersByDefault: true
  },
  purge: [
    './pages/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',
    './src/components/**/*.js',
    './pages/**/*.js'
  ],
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {}
  },
  variants: {
    extend: {}
  },
  plugins: [require('tailwindcss'), require('precss'), require('autoprefixer')]
};
```

### Folha de estilos global
Crie a pasta *styles* na raiz do projeto e dentro dela crie o arquivo *style.scss* e deixe-o assim:

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Alterações no _app.tsx
Altere o arquivo *_app.tsx* e deixe-o assim:

```
import { AppProps } from 'next/dist/next-server/lib/router/router';

import 'styles/styles.scss';

function App({ Component, pageProps }: AppProps): JSX.Element {
  return <Component {...pageProps} />;
}

export default App;
```



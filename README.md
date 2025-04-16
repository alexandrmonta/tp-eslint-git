2 lancer eslint
npx eslint app.js

j'ai modifié le test pour retirer une quote : j'ai une erreur : 

C:\Users\alexm\tp-eslint-git\app.js
  5:17  error  Parsing error: Unterminated string constant      

✖ 1 problem (1 error, 0 warnings)

3 fix manuel, et maintenant : 

PS C:\Users\alexm\tp-eslint-git> npx eslint --fix app.js

C:\Users\alexm\tp-eslint-git\app.js
  0:0  warning  File ignored because of a matching ignore pattern. Use "--no-ignore" to disable file ignore settings or use "--no-warn-ignored" to suppress this warning

✖ 1 problem (0 errors, 1 warning)

PS C:\Users\alexm\tp-eslint-git> npx eslint app.js
PS C:\Users\alexm\tp-eslint-git>

l'erreur à bien disparu

partie 4 : après personnalisation des règles j'ai cette erreur après npm run list: 

PS C:\Users\alexm\tp-eslint-git> npm run lint

> tp-eslint-git@1.0.0 lint
> eslint .


C:\Users\alexm\tp-eslint-git\app.js
  2:1  warning  Unexpected console statement                  no-console
  4:1  error    Expected indentation of 2 spaces but found 4  indent
  4:5  warning  Unexpected console statement                  no-console

✖ 3 problems (1 error, 2 warnings)
  1 error and 0 warnings potentially fixable with the `--fix` option.

PS C:\Users\alexm\tp-eslint-git> npm run lint -- --fix
   
> tp-eslint-git@1.0.0 lint
> eslint .


C:\Users\alexm\tp-eslint-git\app.js
  2:1  warning  Unexpected console statement                  no-console
  4:1  error    Expected indentation of 2 spaces but found 4  indent
  4:5  warning  Unexpected console statement                  no-console

✖ 3 problems (1 error, 2 warnings)
  1 error and 0 warnings potentially fixable with the `--fix` option.

PS C:\Users\alexm\tp-eslint-git> 


eslint.config.mjs que j'ai du modifier : 

import js from '@eslint/js';
import { defineConfig } from 'eslint/config';

export default defineConfig([
  {
    ignores: ['node_modules/', 'dist/'], 
  },
  {
    files: ['*/.js'],
    languageOptions: {
      ecmaVersion: 2021,
      sourceType: 'module',
      globals: {
        browser: true,
        node: true
      }
    },
    rules: {
      'no-console': 'warn',
      'indent': ['error', 2],
      'quotes': ['error', 'single']
    }
  }
]);

package.json que j'ai du modifier :

{
  "name": "tp-eslint-git",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "lint": "eslint ."
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@eslint/json": "^0.11.0",
    "eslint": "^9.24.0",
    "husky": "^9.1.7"
  }
}

j'ai été jusqu'à la 6 Simulation d'un travail d'équipe
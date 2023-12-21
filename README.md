# AptoORM example

## How to use AptoORM?


```bash
# Initialize AptoORM Typescript project
mkdir apto_example
cd apto_example
pnpm init
pnpm i -D typescript @types/node aptos apto_orm ts-node
jq --arg key "build" --arg val "tsc --build" '.scripts[$key]=$val' package.json | jq "." > _package.json && mv _package.json package.json
jq --arg key "apto_orm" --arg val "apto_orm" '.scripts[$key]=$val' package.json | jq "." > _package.json && mv _package.json package.json

{
  echo "{"
  echo '  "compilerOptions": {'
  echo '    "target": "ES2020",'
  echo '    "module": "CommonJS",'
  echo '    "moduleResolution": "node",'
  echo '    "skipLibCheck": true,'
  echo '    "resolveJsonModule": true,'
  echo '    "esModuleInterop": true,'
  echo '    "emitDecoratorMetadata": true,'
  echo '    "experimentalDecorators": true,'
  echo '    "allowSyntheticDefaultImports": true,'
  echo '    "declaration": false,'
  echo '    "outDir": "dist"'
  echo '  },'
  echo '  "include": ["src"],'
  echo '  "exclude": ["node_modules", "**/*.spec.ts"]'
  echo "}"
} > tsconfig.json

{
  echo 'dist'
  echo 'out'
  echo 'build'
  echo 'node_modules'
  echo '**/build'
  echo '.key'
} > .gitignore

# Create AptoORM class
npx apto_orm init src/apto_example --token -c MyToken
npx apto_orm generate src/apto_example
npx apto_orm compile src/apto_example
npx apto_orm create-account -k .key/apto_example --prepay_url http://localhost:5678
npx apto_orm publish src/apto_example -k .key/apto_example --prepay_url http://localhost:5678
npx apto_orm create src/apto_example -k .key/apto_example --prepay_url http://localhost:5678 -c MyToken -d '{ "uri": "http://abc.com", "description": "ok", "id": 123, "name": "ABC" }'
npx apto_orm update src/apto_example -k .key/apto_example --prepay_url http://localhost:5678 -c MyToken -d '{ "uri": "http://abc.com", "description": "fail", "id": 123, "name": "ABC" }'

# Create PoA account
npx apto_orm --prepay_url http://localhost:5678 create-account -r poa1
npx apto_orm --prepay_url http://localhost:5678 poa register -d .key/apto_example -l .key/poa1
npx apto_orm --prepay_url http://localhost:5678 poa show -l .key/poa1
npx apto_orm init src/apto_example --token -c MyToken
npx apto_orm create src/apto_example -k .key/poa1 --prepay_url http://localhost:5678 -c MyToken -d '{ "uri": "http://abc.com", "description": "ok", "id": 1234, "name": "ABC" }'
```

- Typescript project creation: [creating-a-typescript-project](https://dev.to/theoparis/creating-a-typescript-project-47gl)

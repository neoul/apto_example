# AptoORM example

```bash
# Reusable bash function you can add to your ~/.zshrc or ~/.bashrc file
#
# Usage: pkg-script start "node index.js"
#
function pkg-script () {
  echo $(jq --arg key "${1}" --arg val "${2}" '.scripts[$key]=$val' package.json) | jq . > _package.json && mv _package.json package.json
}

pkg-script build "tsc --build"

```

```bash
https://dev.to/theoparis/creating-a-typescript-project-47gl
```

```bash
mkdir apto_example
cd apto_example
pnpm init
pnpm i -D typescript @types/node
jq --arg key "build" --arg val "tsc --build" '.scripts[$key]=$val' package.json | jq "." > _package.json && mv _package.json package.json

{
  echo "{"
  echo '  "compilerOptions": {'
  echo '    "target": "ES2019",'
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
} >> .gitignore


echo $(jq --arg key "build" --arg val "tsc --build" '.scripts[$key]=$val' package.json) | jq . | > package.json
```

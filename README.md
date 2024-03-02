# tsconfig-paths-webpack-plugin kullanarak CRA'da typescript path alias yapılandırması

## tsconfig.json dosyasının yapılandırılması

1. baseUrl:Tüm modül yollarının başlayacağı temel dizini belirtir.
2. paths:Örnek olarak "@/" ile başlayan yolların src ve dist klasörleri altındaki dosyaları içerdiği anlamına gelir.

```
{
  "compilerOptions": {
    // existing options...

    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*", "./dist/*", ""],
      "pages/*": ["src/pages/*"],
      "components/*": ["src/components/*"],
      "types/*": ["src/@types/*"],
      "public/*": ["public/*"]
    }
  }
}
```

Otomatik olarak "@/" yolunu import edebilmek içinde vscode'da
"import module specifier" ayarlarını yapılandırmak gerekiyor.
![noneRelative](public/non-relative.png)

## tsconfig-paths-webpack-plugin kurulumu

```bash
npm install tsconfig-paths-webpack-plugin --save-dev
```

1. node_modules/react-scripts/config/webpack.config.js dosyasını açın,
2. webpack.config.js dosyanızın en üstünde, TsconfigPathsPlugin'i başlatmak için require ifadesini ekleyin
3. Yapılandırma içinde çözümleme bölümünü bulun
4. resolve bölümünün plugins dizisini içerdiğinden emin olun.
5. plugins dizisine new TsconfigPathsPlugin() satırını ekleyin.

```
"Üst tarafa eklenecek kısım"
const TsconfigPathsPlugin = require('tsconfig-paths-webpack-plugin');

"pluginsden sonra çağıralacak kısım"
module.exports = function (webpackEnv) {
...
  return {
  ...
    resolve: {
      ...
      plugins: [
         ...
         // add following line
         new TsconfigPathsPlugin(),
      ]
    }
  }
}
```

## Kaynaklar

[medium](https://medium.com/@umerfaheem67/configuring-typescript-path-alias-in-react-using-tsconfig-paths-webpack-plugin-dbb1b6644bdf)
[stackoverflow](https://stackoverflow.com/questions/77314336/always-use-alias-for-automatic-imports)

---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: service-bus-relay
author: clemensv
ms.service: service-bus-relay
ms.topic: include
ms.date: 05/02/2018
ms.author: clemensv
ms.custom: include file
ms.openlocfilehash: d0fd3e88bdb25fdfd430924ef6b7f571d070b733
ms.sourcegitcommit: 870d372785ffa8ca46346f4dfe215f245931dae1
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/08/2018
ms.locfileid: "33905218"
---
### <a name="create-a-nodejs-application"></a>Tworzenie aplikacji w języku Node.js

Utwórz plik JavaScript o nazwie `listener.js`.

### <a name="add-the-relay-npm-package"></a>Dodawanie pakietu NPM usługi Relay

Uruchom polecenie `npm install hyco-https` w wierszu polecenia języka Node w folderze projektu.

### <a name="write-some-code-to-handle-requests"></a>Tworzenie kodu do obsługi żądań

1. Dodaj następującą stałą na początku pliku `listener.js`.

    ```js
    const https = require('hyco-https');
    ```
2. Dodaj następujące stałe do pliku `listener.js` na potrzeby szczegółów połączenia hybrydowego. Zastąp symbole zastępcze w nawiasach wartościami uzyskanymi podczas tworzenia połączenia hybrydowego.

   1. `const ns` — obszar nazw usługi Relay. Pamiętaj, aby użyć w pełni kwalifikowanej nazwy obszaru nazw, na przykład `{namespace}.servicebus.windows.net`.
   2. `const path` — nazwa połączenia hybrydowego.
   3. `const keyrule` — nazwa klucza sygnatury dostępu współdzielonego.
   4. `const key` — wartość klucza sygnatury dostępu współdzielonego.

3. Dodaj następujący kod do pliku `listener.js`. :

    Zauważysz, że kod nie różni się znacząco od kodu dowolnego prostego serwera HTTP, który możesz znaleźć w samouczkach oprogramowania Node.js dla początkujących, przy czym różnica polega na użyciu funkcji `createRelayedServer` zamiast typowej funkcji `createServer`.

    ```js
    var uri = https.createRelayListenUri(ns, path);
    var server = https.createRelayedServer(
        {
            server : uri,
            token : () => https.createRelayToken(uri, keyrule, key)
        },
        (req, res) => {
            console.log('request accepted: ' + req.method + ' on ' + req.url);
            res.setHeader('Content-Type', 'text/html');
            res.end('<html><head><title>Hey!</title></head><body>Relayed Node.js Server!</body></html>');
        });

    server.listen( (err) => {
            if (err) {
              return console.log('something bad happened', err)
            }
            console.log(`server is listening on ${port}`)
          });

    server.on('error', (err) => {
        console.log('error: ' + err);
    });
    ```
    Plik listener.js powinien wyglądać w następujący sposób:
   
    ```js
    const https = require('hyco-https');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var uri = https.createRelayListenUri(ns, path);
    var server = https.createRelayedServer(
        {
            server : uri,
            token : () => https.createRelayToken(uri, keyrule, key)
        },
        (req, res) => {
            console.log('request accepted: ' + req.method + ' on ' + req.url);
            res.setHeader('Content-Type', 'text/html');
            res.end('<html><head><title>Hey!</title></head><body>Relayed Node.js Server!</body></html>');
        });

    server.listen( (err) => {
            if (err) {
              return console.log('something bad happened', err)
            }
            console.log(`server is listening on ${port}`)
          });

    server.on('error', (err) => {
        console.log('error: ' + err);
    });
    ```


# BitTribe 🪙

## Objetivo
Desarrollar un sistema basado en una base de datos MongoDB para gestionar información relacionada con criptomonedas, usuarios, wallets, transacciones y exchanges, permitiendo el análisis, seguimiento y administración de actividades en un ecosistema de criptomonedas.

## Descripcion
El sistema es una solución integral diseñada para almacenar, consultar y analizar datos relacionados con criptomonedas y sus usuarios. Utiliza una base de datos NoSQL (MongoDB) para manejar cinco colecciones interrelacionadas: criptomonedas, exchanges, users, transacciones y wallets. Estas colecciones permiten gestionar información sobre criptomonedas, plataformas de intercambio, usuarios registrados, transacciones realizadas y wallets asociadas, ofreciendo funcionalidades para análisis financiero, seguimiento de usuarios y auditoría de transacciones. El sistema está diseñado para ser escalable, flexible y adecuado para aplicaciones financieras, exchanges o plataformas de análisis de criptomonedas.

La base de datos representa un sistema de criptomonedas con las siguientes colecciones:
- **Criptomonedas:** Almacena información sobre criptomonedas (Bitcoin, Ethereum, etc.), incluyendo su nombre, símbolo, blockchain, precio actual, capitalización de mercado, suministro máximo y algoritmo.

- **Exchanges:** Contiene datos de plataformas de intercambio (Binance, etc.), con detalles como monedas disponibles, comisiones, volumen diario y número de usuarios registrados.

- **Users:** Registra información de usuarios, incluyendo nombre, email, país, wallets asociadas y cuentas en exchanges.

- **Transacciones:** Guarda detalles de transacciones entre wallets, incluyendo la criptomoneda transferida, direcciones de origen y destino, cantidad, comisión y fecha.

- **Wallets:** Almacena las wallets de los usuarios, con su dirección, criptomoneda asociada, balance y el ID del usuario propietario.


## Cómo crear la base de datos desde MongoDB
1. Crear la base de datos
    ```
    use BitTripe
    ```
2. Crear la coleccion criptoCoins, users, wallets, transacciones, exchanges
    ```
    db.createCollection("criptoCoins")
    db.createCollection("users")
    db.createCollection("wallets")
    db.createCollection("transacciones")
    db.createCollection("exchanges")
    ```
3. Importar JSON de cada coleccion
    - *coleccion_criptoCoins.json* en la coleccion **criptoCoins**
    - *coleccion_users.json* en la coleccion **users**
    - *coleccion_wallets.json* en la coleccion **wallets**
    - *coleccion_transacciones.json* en la coleccion **transacciones**
    - *coleccion_exchanges.json* en la coleccion **exchanges**

    ![alt text](<Captura desde 2025-06-12 22-29-10.png>)


## Consultas

### Consulta 1: 
#### Buscar criptomonedas cuyo nombre empiece por "Sh"

```
db.criptoCoins.find({ "nombre": { "$regex": "^Sh", "$options": "i" } })
```
Esta consulta es útil en el buscador inteligente de BitTribe. Permite que al escribir las primeras letras de una criptomoneda, como "Shiba Inu" o "Shiden Network", el sistema pueda mostrar sugerencias en tiempo real. Esto mejora la experiencia del usuario, reduce errores de tipeo y acelera el proceso de búsqueda.


### Consulta 2: 
####  Buscar criptomonedas cuyo símbolo empiece con "B"

```
db.criptomonedas.find({ "simbolo": { "$regex": "^B" } })
```
BitTribe podría usar esta consulta para ofrecer filtros alfabéticos o listas rápidas de monedas por símbolo, por ejemplo todas las que comienzan por “B” como BTC, BNB, BAT. Esto también es útil en interfaces móviles donde se muestran listas categorizadas o para generar menús de navegación rápida por inicial.


### Consulta 3: 
####  Buscar usuarios cuyo correo contenga "mail"

```
db.usuarios.find({ "email": { "$regex": "mail", "$options": "i" } })
```
 Permite conocer la proporción de usuarios que usan correos de Gmail, lo cual puede ser útil para estadísticas internas, pruebas A/B, o incluso adaptar validaciones o recomendaciones de seguridad. También puede ayudar en campañas promocionales o segmentadas si se desea enviar correos.


### Consulta 4: 
####  Buscar usuarios cuyo nombre comience con "Mar"

```
db.users.find({ nombre: { $regex: /^Mar/i } })
```
Ideal para autocompletado de nombres al buscar amigos o contactos.


### Consulta 5: 
####  Filtrar usuarios con nombres compuestos (contienen espacio)

```
db.users.find({ nombre: { $regex: /\s+/ } })
```
Para visualizaciones personalizadas del nombre completo.



### Consulta 6: 
####  Encontrar wallets con cripto que empiece por "btc" (Bitcoin)

```
db.wallets.find({ cripto: { $regex: /^btc/i } })
```
Para identificar rápidamente wallets de BTC.


### Consulta 7: 
####  Buscar criptomonedas cuyo nombre contenga la palabra "coin"

```
db.criptoCoins.find({ nombre: { $regex: "coin", $options: "i" } })

```
Mostrar al usuario monedas populares que incluyan "coin", como "Bitcoin", "Binance Coin" o "Dogecoin".


### Consulta 8: 
####  Encontrar criptomonedas cuyo símbolo tenga exactamente 3 letras mayúsculas

```
db.criptoCoins.find({ simbolo: { $regex: "^[A-Z]{3}$" } })

```
 Filtrar criptos tradicionales y más establecidas como "BTC", "ETH", "LTC", útiles en filtros avanzados.


### Consulta 9: 
####  Criptomonedas en blockchains que empiecen con la letra "E"

```
db.criptoCoins.find({ blockchain: { $regex: "^E", $options: "i" } })

```
 Para mostrar al usuario tokens y criptos basadas en Ethereum o similares.


### Consulta 10: 
####  Criptos cuyo tipo sea un token (usando RegEx flexible)

```
db.criptomonedas.find({ "simbolo": { "$regex": "^B" } })
```
Filtrar solo tokens para recomendaciones en wallets tipo ERC-20 o compatibles.


### Consulta 11: 
#### Buscar criptomonedas que utilicen algoritmos que incluyan "Stake"

```
db.criptoCoins.find({ algoritmo: { $regex: "Stake", $options: "i" } })

```
Ayuda a los usuarios interesados en participar en staking a encontrar criptos compatibles.


### Consulta 12: 
#### Criptomonedas cuyo nombre comience con "D"

```
db.criptoCoins.find({ nombre: { $regex: "^D", $options: "i" } })

```
Para buscar rápidamente criptos como "Dash" o "Dogecoin" desde el buscador.


### Consulta 13: 
####  Criptomonedas cuyo nombre contiene exactamente dos palabras

```
db.criptoCoins.find({ nombre: { $regex: "^[A-Za-z]+\\s[A-Za-z]+$" } })

```
Para visualización o análisis de branding de criptos con nombres compuestos como "Binance Coin".


### Consulta 14: 
####  Buscar exchanges cuyo país comience con “Es” (como “Estados Unidos”)

```
db.exchanges.find({ pais: { $regex: /^Es/, $options: 'i' } })

```
Filtrar exchanges ubicados en países específicos (útil en filtros geográficos para el usuario).


### Consulta 15: 
####  Encontrar exchanges que ofrezcan monedas que empiecen con la letra "D" (como DOGE o DOT)

```
db.exchanges.find({ monedasDisponibles: { $elemMatch: { $regex: /^D/, $options: 'i' } } })

```
Mostrar a los usuarios qué exchanges permiten comprar criptomonedas de moda como DOGE o DOT.


### Consulta 16: 
####   Listar exchanges con nombre que termine en “ex” (como “Rippex”)

```
db.exchanges.find({ nombre: { $regex: /ex$/, $options: 'i' } })

```
Permitir búsquedas flexibles por nombre en tu buscador (autocomplete, sugerencias, etc.).


### Consulta 17: 
####  Buscar exchanges con monedas soportadas en la red Ethereum (tokens como SHIB, UNI, ETH)

```
db.exchanges.find({ monedasDisponibles: { $in: [/^ETH$|^SHIB$|^UNI$/] } })

```
Filtrar exchanges por red específica para mostrar compatibilidad de tokens ERC-20.


### Consulta 18: 
####  Identificar exchanges en países que contengan “Caimán” (Islas Caimán)

```
db.exchanges.find({ pais: { $regex: /Caimán/i } })

```
Mostrar exchanges por región fiscal o regulatoria (por ejemplo, para usuarios que buscan anonimato o beneficios fiscales).


### Consulta 19: 
####  Listar exchanges cuyo volumen diario supere los 5 mil millones y tengan nombre que empiece por “B”

```
db.exchanges.find({ 
  volumenDiarioUSD: { $gte: 5000000000 },
  nombre: { $regex: /^B/i }
})

```
Promocionar exchanges grandes y populares, útiles para traders profesionales.


### Consulta 20: 
####  Buscar exchanges con comisiones de compra menores al 0.2% y nombre que contenga "ku"

```
db.exchanges.find({
  "comisiones.compra": { $lt: 0.2 },
  nombre: { $regex: /ku/i }
})

```
Recomendar exchanges más baratos a usuarios novatos o que desean minimizar gastos.


### Consulta 21: 
####  Buscar transacciones recibidas por direcciones que incluyen “SHIB”

```
db.transacciones.find({ para: { $regex: "SHIB", $options: "i" } })

```
para rastrear a quienes están acumulando o reciben SHIB, útil para analítica o recomendaciones.


### Consulta 22: 
####  Transacciones que involucran usuarios con nombres que empiezan por “0xJavi”

```
db.transacciones.find({ de: { $regex: "^0xJavi" } })

```
Filtra el historial de un usuario específico o con un patrón de alias personalizable.

### Consulta 23: 
####  Filtrar transacciones de direcciones con alias que terminan en un número impar



```
db.transacciones.find({ de: { $regex: "[13579]$" } })

```
Útil para análisis de segmentos de usuarios si los identificadores tienen lógica interna.


### Consulta 24: 
####  Usuarios con direcciones de wallet que terminan en números

```
db.users.find({ "wallets.direccion": { $regex: /\d+$/, $options: 'i' } })

```
Detecta direcciones como 0xFerXRP111 o 0xTomiADA77.


### Consulta 25: 
####  Países que terminan en “a”

```
db.users.find({ pais: { $regex: /a$/i } })

```
Traera todos los paises que comienzen con A esto servira cuanado necesite consultar datos limitados


### Consulta 26: 
####  Buscar wallets de usuarios con dirección que contenga “Rey” (como IsaRey456)

```
db.wallets.find({ direccion: { $regex: "Rey" } })

```
Un usuario con el alias "Rey" reportó un error con su wallet. Busco todas las direcciones que contienen “Rey” para hacer un seguimiento manual.
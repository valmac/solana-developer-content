---
sidebarLabel: Быстрый старт
title: Краткое руководство Solana
sidebarSortOrder: 1
---

Добро пожаловать в краткое руководство Solana! 
Это практическое руководство познакомит вас с основными концепциями 
разработки на Solana, независимо от вашего предыдущего опыта. 
К концу этого руководства вы получите базовые знания по разработке Solana 
и будете готовы к изучению более сложных тем.

## Что вы узнаете

В этом уроке вы узнаете о:

- Понимание учетных записей: узнайте, как данные хранятся в сети Solana.
- Отправка транзакций: научитесь взаимодействовать с сетью Solana, отправляя транзакции.
- Создание и развертывание программ: создайте свою первую программу Solana и разверните ее в сети.
- Адреса, производные от программы (PDA). Узнайте, как использовать PDA для создания
  детерминированные адреса для учетных записей.
- Межпрограммные вызовы (CPI): узнайте, как заставить ваши программы взаимодействовать с другими программами на Solana.

Лучшая часть? Вам не нужно ничего устанавливать! Мы будем использовать 
Solana Playground — браузерная среда разработки для всех наших примеров. 
Это означает, что вы можете следовать инструкциям, копировать и вставлять код 
и немедленно видеть результаты, и все это в вашем веб-браузере. 
Базовые знания программирования полезны, но не обязательны.

Давайте погрузимся и начнем строить Солану!

## Solana Playground

Solana Playground (Solpg) — это браузерная среда разработки, 
позволяющая быстро разрабатывать, развертывать и тестировать программы Solana!

Откройте новую вкладку в веб-браузере и перейдите по адресу https://beta.solpg.io/.

<Steps>

### Создать кошелек Solana Playground

Если вы новичок в Solana Playground, первым шагом будет создание кошелька 
Playground. Этот кошелек позволит вам взаимодействовать с сетью Solana 
прямо из браузера.

#### Шаг 1. Подключитесь к игровой площадке

Нажмите кнопку «Не подключено» в левом нижнем углу экрана.

![Not Connected](/assets/docs/intro/quickstart/pg-not-connected.png)

#### Шаг 2. Создайте свой кошелек

Вы увидите возможность сохранить пару ключей вашего кошелька. 
При желании сохраните пару ключей вашего кошелька для 
резервного копирования и нажмите «Продолжить».

![Create Playground Wallet](/assets/docs/intro/quickstart/pg-create-wallet.png)

Теперь вы должны увидеть адрес вашего кошелька, баланс SOL и 
подключенный кластер (по умолчанию devnet) в нижней части окна.

![Connected](/assets/docs/intro/quickstart/pg-connected.png)

<Callout>
  Ваш кошелек Playground будет сохранен в локальном хранилище вашего браузера. 
  Очистка кеша браузера приведет к удалению сохраненного кошелька.
</Callout>

### Получить доступ к Devnet SOL

Прежде чем мы начнем сборку, нам сначала понадобится немного devnet SOL.

С точки зрения разработчика, SOL необходим для двух основных случаев использования:

- Для создания учетных записей, где мы можем хранить данные или развертывать программы.
- Для оплаты комиссий за транзакции при взаимодействии с сетью

Ниже приведены два способа пополнить свой кошелек с помощью devnet SOL:

#### Вариант 1. Использование терминала игровой площадки

Чтобы пополнить свой кошелек Playground с помощью devnet SOL. В терминале Playground запустите:

```shell filename="Terminal"
solana airdrop 5
```

#### Вариант 2. Использование крана Devnet

Если команда airdrop не работает (из-за ограничений скорости или ошибок), 
вы можете использовать [Веб-сборщик (Web Faucet)](https://faucet.solana.com/).

- Введите адрес своего кошелька (находится внизу экрана игровой площадки) и выберите сумму.
- Нажмите «Подтвердить раздачу», чтобы получить SOL devnet.
![Faucet Airdrop](/assets/docs/intro/quickstart/faucet-airdrop.gif)

</Steps>

## Чтение из сети

Теперь давайте рассмотрим, как читать данные из сети Solana. Мы возьмем 
несколько разных учетных записей, чтобы понять структуру учетной записи Solana.

В Solana все данные содержатся в так называемых «учетных записях». 
Вы можете думать о данных Solana как об общедоступной базе данных 
с одной таблицей «Счета», где каждая запись в этой таблице представляет собой 
отдельную учетную запись.

Учетные записи на Solana могут хранить «состоятельные» или «исполняемые» программы, 
все из которых можно рассматривать как записи в одной и той же таблице «Учетные записи». 
Каждая учетная запись имеет «адрес» (открытый ключ), который служит ее 
уникальным идентификатором, используемым для поиска соответствующих данных в цепочке.

Учетные записи Solana содержат:

- Состояние: это данные, которые предназначены для чтения и сохранения. Это может быть 
  информация о токенах, пользовательских данных или любой другой тип данных, 
  определенный в программе.
- Исполняемые программы: это учетные записи, содержащие реальный код программ Solana. 
  Они содержат инструкции, которые могут выполняться в сети.

Такое разделение программного кода и состояния программы является ключевой особенностью 
модели учетной записи Solana. Для получения более подробной информации см.
Страница [Модель учетной записи Solana](/docs/core/accounts).

<Steps>

### Принести кошелек для игровой площадки

Начнем с рассмотрения знакомого аккаунта — вашего собственного кошелька Playground! 
Мы получим эту учетную запись и исследуем ее структуру, чтобы понять, 
как выглядит базовая учетная запись Solana.

#### Шаг 1. Откройте пример

Нажмите эту [ссылку](https://beta.solpg.io/6671c5e5cffcf4b13384d198), 
чтобы открыть пример в Solana Playground. Вы увидите этот код:

```ts filename="client.ts"
const address = pg.wallet.publicKey;
const accountInfo = await pg.connection.getAccountInfo(address);

console.log(JSON.stringify(accountInfo, null, 2));
```

<details>
{<summary>Explanation</summary>}

This code does three simple things:

- Получает адрес вашего кошелька Playground.

  ```ts
  const address = pg.wallet.publicKey;
  ```

- Получает `AccountInfo` для учетной записи по этому адресу.

  ```ts
  const accountInfo = await pg.connection.getAccountInfo(address);
  ```

- Распечатывает `AccountInfo` на терминал Playground.

  ```ts
  console.log(JSON.stringify(accountInfo, null, 2));
  ```

</details>

#### Шаг 2. Запустите код

В терминале Playground введите команду «run» и нажмите Enter:

```shell filename="Terminal"
run
```

Вы должны увидеть подробную информацию о своем счете кошелька, 
включая его баланс в лампортах, с выводом, аналогичным следующему:

<details>
{<summary>Output</summary>}

```shell filename="Terminal"
$ run
Running client...
  client.ts:
    {
  "data": {
    "type": "Buffer",
    "data": []
  },
  "executable": false,
  "lamports": 5000000000,
  "owner": "11111111111111111111111111111111",
  "rentEpoch": 18446744073709552000,
  "space": 0
}
```

</details>

<details>
{<summary>Explanation</summary>}

Ваш кошелек на самом деле представляет собой просто учетную запись, 
принадлежащую Системной программе, где основной целью учетной записи 
кошелька является хранение вашего баланса SOL (сумма в поле «lamports»).

---

По своей сути все учетные записи Solana представлены в стандартном формате, 
называемом AccountInfo. Тип данных 
[AccountInfo](https://github.com/solana-labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/account_info.rs#L19-L36) 
является базовой структурой данных для всех учетных записей Solana.

Давайте разберем поля в выводе:

- `данные`. Это поле содержит то, что мы обычно называем «данными» учетной записи. 
   Для кошелька оно пустое (0 байт), но другие учетные записи используют это поле 
   для хранения любых произвольных данных в виде сериализованного буфера байтов.
- `исполняемый` — флаг, указывающий, является ли учетная запись исполняемой программой. 
   Для кошельков и любых учетных записей, хранящих состояние, это «ложь».
- `владелец` - В этом поле показано, какая программа управляет учетной записью. 
   Для кошельков это всегда Системная программа с адресом `111111111111111111111111111111111`.
- `лампорты` - Баланс счета в лампортах (1 SOL = 1 000 000 000 лампортов).
- `rentEpoch` — устаревшее поле, связанное с устаревшим механизмом сбора арендной платы Solana 
   (в настоящее время не используется).
- `space` – указывает емкость (длину) поля `data` в байтах, но не является полем типа `AccountInfo`.

</details>

### Программа получения токенов

Далее мы рассмотрим программу Token Extensions — исполняемую программу 
для взаимодействия с токенами на Solana.

#### Шаг 1: Откройте пример

Щелкните эту [ссылку](https://beta.solpg.io/6671c6e7cffcf4b13384d199), 
чтобы открыть пример в Solana Playground. Вы увидите этот код:

```ts filename="client.ts" {3}
import { PublicKey } from "@solana/web3.js";

const address = new PublicKey("TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb");
const accountInfo = await pg.connection.getAccountInfo(address);

console.log(JSON.stringify(accountInfo, null, 2));
```

Вместо получения вашего кошелька Playground мы получаем адрес учетной записи 
программы расширения токенов.

#### Шаг 2. Запустите код

Запустите код с помощью команды «run» в терминале.

```shell filename="Terminal"
run
```

Изучите выходные данные и то, чем эта учетная запись программы 
отличается от учетной записи вашего кошелька.

<details>
{<summary>Output</summary>}

```shell filename="Terminal" {15, 17}
$ run
Running client...
  client.ts:
    {
  "data": {
    "type": "Buffer",
    "data": [
      2,
      0,
      //... additional bytes
      86,
      51
    ]
  },
  "executable": true,
  "lamports": 1141440,
  "owner": "BPFLoaderUpgradeab1e11111111111111111111111",
  "rentEpoch": 18446744073709552000,
  "space": 36
}
```

</details>

<details>
{<summary>Explanation</summary>}

Программа Token Extensions представляет собой исполняемую учетную запись 
программы, но учтите, что она имеет ту же структуру AccountInfo.

Ключевые отличия в AccountInfo:

- `executable` — установлено значение `true`, указывающее, 
   что эта учетная запись представляет собой исполняемую программу.
- `data` - Содержит сериализованные данные (в отличие от пустых данных 
   в учетной записи кошелька). В данных учетной записи программы хранится адрес 
   другой учетной записи (учетной записи исполняемых данных программы), 
   которая содержит байт-код программы.
- `owner` — учетная запись принадлежит обновляемому загрузчику BPF 
  (`BPFLoaderUpgradeab1e11111111111111111111111`), специальной программе, 
  которая управляет исполняемыми учетными записями.---

Вы можете проверить Solana Explorer для 
[учетной записи программы расширений токенов] (https://explorer.solana.com/address/TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb)
и соответствующую ему 
[Учетную запись исполняемых данных программы] (https://explorer.solana.com/address/DoU57AYuPFu2QU514RktNPG22QhApEjnKxnBcu4BHDTY).

Учетная запись исполняемых данных программы содержит скомпилированный 
байт-код для программы расширений токенов.
[source code](https://github.com/solana-labs/solana-program-library/tree/b1c44c171bc95e6ee74af12365cb9cbab68be76c/token/program-2022/src).

</details>

### Получить учетную запись Mint

На этом этапе мы рассмотрим учетную запись Mint, которая представляет собой 
уникальный токен в сети Solana.

#### Шаг 1. Откройте пример

Щелкните эту [ссылку](https://beta.solpg.io/6671c9aecffcf4b13384d19a), 
чтобы открыть пример в Solana Playground. Вы увидите этот код:

```ts filename="client.ts" {3}
import { PublicKey } from "@solana/web3.js";

const address = new PublicKey("C33qt1dZGZSsqTrHdtLKXPZNoxs6U1ZBfyDkzmj6mXeR");
const accountInfo = await pg.connection.getAccountInfo(address);

console.log(JSON.stringify(accountInfo, null, 2));
```

В этом примере мы получим адрес существующей учетной записи Mint в devnet.

#### Шаг 2. Запустите код

Запустите код с помощью команды «Выполнить».

```shell filename="Terminal"
run
```

<details>
{<summary>Output</summary>}

```shell filename="Terminal" {17}
$ run
Running client...
  client.ts:
    {
  "data": {
    "type": "Buffer",
    "data": [
      1,
      0,
      //... additional bytes
      0,
      0
    ]
  },
  "executable": false,
  "lamports": 4176000,
  "owner": "TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb",
  "rentEpoch": 18446744073709552000,
  "space": 430
}
```

</details>

<details>
{<summary>Explanation</summary>}

Ключевые отличия в AccountInfo:

- `owner` — учетная запись монетного двора принадлежит программе 
  Token Extensions (`TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb`).
- `executable` — установите значение `false`, так как эта учетная запись 
  хранит состояние, а не исполняемый код.
- `data`: Содержит сериализованные данные о токене 
  (правитель монетного двора, поставка, десятичные числа и т. д.).

</details>

#### Шаг 3. Десериализация данных учетной записи Mint

Чтобы прочитать поле data из любой учетной записи, вам необходимо 
десериализовать буфер данных в ожидаемый тип данных. 
Часто это делается с помощью вспомогательных функций 
из клиентских библиотек для конкретной программы.

Откройте следующий [пример](https://beta.solpg.io/6671cd8acffcf4b13384d19b) 
на игровой площадке Solana. Вы увидите этот код:

```ts filename="client.ts"
import { PublicKey } from "@solana/web3.js";
import { getMint, TOKEN_2022_PROGRAM_ID } from "@solana/spl-token";

const address = new PublicKey("C33qt1dZGZSsqTrHdtLKXPZNoxs6U1ZBfyDkzmj6mXeR");
const mintData = await getMint(
  pg.connection,
  address,
  "confirmed",
  TOKEN_2022_PROGRAM_ID,
);

console.log(mintData);
```

В этом примере используется вспомогательная функция getMint 
для автоматической десериализации поля данных учетной записи Mint.

Запустите код с помощью команды «Выполнить».

```shell filename="Terminal"
run
```

Вы должны увидеть следующие десериализованные данные учетной записи Mint.

<details>
{<summary>Output</summary>}

```shell filename="Terminal"
Running client...
  client.ts:
  { address: { _bn: { negative: 0, words: [Object], length: 10, red: null } },
  mintAuthority: { _bn: { negative: 0, words: [Object], length: 10, red: null } },
  supply: {},
  decimals: 2,
  isInitialized: true,
  freezeAuthority: null,
  tlvData: <Buffer 12 00 40 00 2c 5b 90 b2 42 0c 89 a8 fc 3b 2f d6 15 a8 9d 1e 54 4f 59 49 e8 9e 35 8f ab 88 64 9f 5b db 9c 74 a3 f6 ee 9f 21 a9 76 43 8a ee c4 46 43 3d ... > }
```

</details>

<details>
{<summary>Explanation</summary>}

Функция getMint десериализует данные учетной записи в 
[Mint](https://github.com/solana-labs/solana-program-library/blob/b1c44c171bc95e6ee74af12365cb9cbab68be76c/token/program/src/state.rs#L18-L32 ) 
тип данных, определенный в исходном коде программы Token Extensions.

- `address` - адрес учетной записи Mint
- `mintAuthority` — полномочия, разрешающие чеканить новые токены.
- `supply` - Общий запас токенов
- `decimals` — количество десятичных знаков для токена.
- `isInitialized` — были ли инициализированы данные Mint
- `freezeAuthority` — орган, разрешивший замораживать токены-аккаунты.
- `tlvData` — дополнительные данные для расширений токенов (требуется дополнительная информация).
 десериализация)

Вы можете просмотреть полностью десериализованные данные 
[Mint Account](https://explorer.solana.com/address/C33qt1dZGZSsqTrHdtLKXPZNoxs6U1ZBfyDkzmj6mXeR?cluster=devnet), 
включая включенные расширения токенов, в Solana Explorer.

</details>

</Steps>

## Запись в сеть

Теперь, когда мы изучили чтение из сети Solana, давайте научимся записывать в нее данные. 
В Solana мы взаимодействуем с сетью, отправляя транзакции, состоящие из инструкций. 
Эти инструкции определяются программами, которые содержат бизнес-логику того, 
как следует обновлять учетные записи.

Давайте рассмотрим две распространенные операции: передачу SOL и создание токена, 
чтобы продемонстрировать, как создавать и отправлять транзакции. 
Более подробную информацию можно найти на страницах 
[Транзакции и инструкции](/docs/core/transactions) и [Комиссии на Solana](/docs/core/fees).

<Steps>

### Трансфер СОЛ

Мы начнем с простого перевода SOL с вашего кошелька на другой аккаунт. 
Для этого необходимо вызвать команду передачи в системной программе.

Щелкните эту [ссылку](https://beta.solpg.io/6671d85ecffcf4b13384d19e), 
чтобы открыть пример в Solana Playground. Вы увидите этот код:

```ts filename="client.ts"
import {
  LAMPORTS_PER_SOL,
  SystemProgram,
  Transaction,
  sendAndConfirmTransaction,
  Keypair,
} from "@solana/web3.js";

const sender = pg.wallet.keypair;
const receiver = new Keypair();

const transferInstruction = SystemProgram.transfer({
  fromPubkey: sender.publicKey,
  toPubkey: receiver.publicKey,
  lamports: 0.01 * LAMPORTS_PER_SOL,
});

const transaction = new Transaction().add(transferInstruction);

const transactionSignature = await sendAndConfirmTransaction(
  pg.connection,
  transaction,
  [sender],
);

console.log(
  "Transaction Signature:",
  `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
);
```

<details>
{<summary>Explanation</summary>}

Этот скрипт делает следующее:

- Установите свой кошелек Playground в качестве отправителя.

  ```ts
  const sender = pg.wallet.keypair;
  ```

- Создает новую пару ключей в качестве получателя

  ```ts
  const receiver = new Keypair();
  ```

- Создает инструкцию передачи для передачи 0,01 SOL.

  ```ts
  const transferInstruction = SystemProgram.transfer({
    fromPubkey: sender.publicKey,
    toPubkey: receiver.publicKey,
    lamports: 0.01 * LAMPORTS_PER_SOL,
  });
  ```

- Создает транзакцию, включая инструкцию по переводу

  ```ts
  const transaction = new Transaction().add(transferInstruction);
  ```

- Отправляет и подтверждает транзакцию

  ```ts
  const transactionSignature = await sendAndConfirmTransaction(
    pg.connection,
    transaction,
    [sender],
  );
  ```

- Распечатывает ссылку на SolanaFM explorer в терминале Playground 
  для просмотра деталей транзакции.

  ```ts
  console.log(
    "Transaction Signature:",
    `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
  );
  ```

</details>

Запустите код с помощью команды «run».

```shell filename="Terminal"
run
```

Нажмите на ссылку вывода, чтобы просмотреть детали транзакции в проводнике SolanaFM.

<details>
{<summary>Output</summary>}

```shell filename="Terminal"
Running client...
  client.ts:
    Transaction Signature: https://solana.fm/tx/he9dBwrEPhrfrx2BaX4cUmUbY22DEyqZ837zrGrFRnYEBmKhCb5SvoaUeRKSeLFXiGxC8hFY5eDbHqSJ7NYYo42?cluster=devnet-solana
```

</details>

![Transfer SOL](/assets/docs/intro/quickstart/transfer-sol.png)

Вы только что отправили свою первую транзакцию на Solana! 
Обратите внимание, как мы создали инструкцию, добавили ее в транзакцию, 
а затем отправили эту транзакцию в сеть. Это основной процесс 
построения любой транзакции.

### Создать токен

Теперь давайте создадим новый токен, создав и инициализировав 
учетную запись Mint. Для этого необходимы две инструкции:

- Вызовите системную программу, чтобы создать новую учетную запись.
- Вызов программы расширений токенов

Щелкните эту [ссылку](https://beta.solpg.io/6671da4dcffcf4b13384d19f), 
чтобы открыть пример в Solana Playground. Вы увидите следующий код:

```ts filename="client.ts"
import {
  Connection,
  Keypair,
  SystemProgram,
  Transaction,
  clusterApiUrl,
  sendAndConfirmTransaction,
} from "@solana/web3.js";
import {
  MINT_SIZE,
  TOKEN_2022_PROGRAM_ID,
  createInitializeMint2Instruction,
  getMinimumBalanceForRentExemptMint,
} from "@solana/spl-token";

const wallet = pg.wallet;
const connection = new Connection(clusterApiUrl("devnet"), "confirmed");

// Generate keypair to use as address of mint account
const mint = new Keypair();

// Calculate minimum lamports for space required by mint account
const rentLamports = await getMinimumBalanceForRentExemptMint(connection);

// Instruction to create new account with space for new mint account
const createAccountInstruction = SystemProgram.createAccount({
  fromPubkey: wallet.publicKey,
  newAccountPubkey: mint.publicKey,
  space: MINT_SIZE,
  lamports: rentLamports,
  programId: TOKEN_2022_PROGRAM_ID,
});

// Instruction to initialize mint account
const initializeMintInstruction = createInitializeMint2Instruction(
  mint.publicKey,
  2, // decimals
  wallet.publicKey, // mint authority
  wallet.publicKey, // freeze authority
  TOKEN_2022_PROGRAM_ID,
);

// Build transaction with instructions to create new account and initialize mint account
const transaction = new Transaction().add(
  createAccountInstruction,
  initializeMintInstruction,
);

const transactionSignature = await sendAndConfirmTransaction(
  connection,
  transaction,
  [
    wallet.keypair, // payer
    mint, // mint address keypair
  ],
);

console.log(
  "\nTransaction Signature:",
  `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
);

console.log(
  "\nMint Account:",
  `https://solana.fm/address/${mint.publicKey}?cluster=devnet-solana`,
);
```

<details>
{<summary>Explanation</summary>}

Этот скрипт выполняет следующие шаги:

- Настраивает кошелек Playground и подключение к сети разработчиков Solana.

  ```ts
  const wallet = pg.wallet;
  const connection = new Connection(clusterApiUrl("devnet"), "confirmed");
  ```

- Генерирует новую пару ключей для учетной записи mint.

  ```ts
  const mint = new Keypair();
  ```

- Рассчитывает минимальное количество лампортов, необходимое 
  для учетной записи Mint.

  ```ts
  const rentLamports = await getMinimumBalanceForRentExemptMint(connection);
  ```

- Создает инструкцию по созданию новой учетной записи для монетного двора, 
  указывая программу Token Extensions (`TOKEN_2022_PROGRAM_ID`) 
  в качестве владельца новой учетной записи.

  ```ts
  const createAccountInstruction = SystemProgram.createAccount({
    fromPubkey: wallet.publicKey,
    newAccountPubkey: mint.publicKey,
    space: MINT_SIZE,
    lamports: rentLamports,
    programId: TOKEN_2022_PROGRAM_ID,
  });
  ```

- Создает инструкцию для инициализации данных учетной записи монетного двора.

  ```ts
  const initializeMintInstruction = createInitializeMint2Instruction(
    mint.publicKey,
    2,
    wallet.publicKey,
    wallet.publicKey,
    TOKEN_2022_PROGRAM_ID,
  );
  ```

- Добавляет обе инструкции в одну транзакцию

  ```ts
  const transaction = new Transaction().add(
    createAccountInstruction,
    initializeMintInstruction,
  );
  ```

- Отправляет и подтверждает транзакцию. И кошелек, и пара ключей mint 
  передаются в качестве подписывающих сторон транзакции. 
  Кошелек необходим для оплаты создания новой учетной записи. 
  Требуется пара ключей mint, поскольку мы используем ее открытый ключ 
  в качестве адреса новой учетной записи.

  ```ts
  const transactionSignature = await sendAndConfirmTransaction(
    connection,
    transaction,
    [wallet.keypair, mint],
  );
  ```

- Распечатывает ссылки для просмотра сведений о транзакции и счете на SolanaFM.

  ```ts
  console.log(
    "\nTransaction Signature:",
    `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
  );

  console.log(
    "\nMint Account:",
    `https://solana.fm/address/${mint.publicKey}?cluster=devnet-solana`,
  );
  ```

</details>

Запустите код с помощью команды `run`.

```shell filename="Terminal"
run
```

Вы увидите две ссылки, напечатанные на терминале Playground:

- Один для деталей транзакции
- Один для вновь созданной учетной записи монетного двора

Нажмите на ссылку, чтобы просмотреть детали транзакции и вновь 
созданную учетную запись монетного двора на SolanaFM.

<details>
{<summary>Output</summary>}

```shell filename="Terminal"
Running client...
  client.ts:

Подпись транзакции: https://solana.fm/tx/3BEjFxqyGwHXWSrEBnc7vTSaXUGDJFY1Zr6L9iwLrjH8KBZdJSucoMrFUEJgWrWVRYzrFvbjX8TmxKUV88oKr86g?cluster=devnet-solana

Mint Account: https://solana.fm/address/CoZ3Nz488rmATDhy1hPk5fvwSZaipCngvf8rYBYVc4jN?cluster=devnet-solana
```

</details>

![Create Token](/assets/docs/intro/quickstart/create-token.png)

![Mint Account](/assets/docs/intro/quickstart/mint-account.png)

Обратите внимание, как на этот раз мы создали транзакцию с несколькими инструкциями. 
Сначала мы создали новую учетную запись, а затем инициализировали ее данные 
как монетный двор. Таким образом вы строите более сложные транзакции, 
включающие инструкции из нескольких программ.

</Steps>

## Deploying Your First Solana Program

В этом разделе мы создадим, развернем и протестируем простую 
программу Solana с использованием платформы Anchor. 
К концу вы развернете свою первую программу в блокчейне Solana!

Цель этого раздела – познакомить вас с игровой площадкой Солана. 
Мы рассмотрим более подробный пример в разделах PDA и CPI. 
Более подробную информацию можно найти на странице 
[Программы на Solana](/docs/core/programs).

<Steps>

### Создать якорный проект

Сначала откройте https://beta.solpg.io в новой вкладке браузера.

- Нажмите кнопку «Создать новый проект» на левой боковой панели.

- Введите имя проекта, выберите Anchor в качестве основы, затем нажмите кнопку «Создать».

![New Project](/assets/docs/intro/quickstart/pg-new-project.gif)

Вы увидите новый проект, созданный с помощью программного кода в файле `src/lib.rs`.

```rust filename="lib.rs"
use anchor_lang::prelude::*;

// This is your program's public key and it will update
// automatically when you build the project.
declare_id!("11111111111111111111111111111111");

#[program]
mod hello_anchor {
    use super::*;
    pub fn initialize(ctx: Context<Initialize>, data: u64) -> Result<()> {
        ctx.accounts.new_account.data = data;
        msg!("Changed data to: {}!", data); // Message will show up in the tx logs
        Ok(())
    }
}

#[derive(Accounts)]
pub struct Initialize<'info> {
    // We must specify the space in order to initialize an account.
    // First 8 bytes are default account discriminator,
    // next 8 bytes come from NewAccount.data being type u64.
    // (u64 = 64 bits unsigned integer = 8 bytes)
    #[account(init, payer = signer, space = 8 + 8)]
    pub new_account: Account<'info, NewAccount>,
    #[account(mut)]
    pub signer: Signer<'info>,
    pub system_program: Program<'info, System>,
}

#[account]
pub struct NewAccount {
    data: u64
}
```

<details>
{<summary>Explanation</summary>}

На данный момент мы рассмотрим только общий обзор программного кода:

- Макрос `declare_id!` указывает адрес вашей программы в цепочке. 
  Он будет автоматически обновлен, когда мы создадим программу на следующем этапе.

  ```rs
  declare_id!("11111111111111111111111111111111");
  ```

- Макрос `#[program]` аннотирует модуль, содержащий функции, 
  которые представляют инструкции программы..

  ```rs
  #[program]
  mod hello_anchor {
      use super::*;
      pub fn initialize(ctx: Context<Initialize>, data: u64) -> Result<()> {
          ctx.accounts.new_account.data = data;
          msg!("Changed data to: {}!", data); // Message will show up in the tx logs
          Ok(())
      }
  }
  ```

  В этом примере инструкция инициализации принимает два параметра:

 1. `ctx: Context<Initialize>` — обеспечивает доступ к учетным записям, 
    необходимым для этой инструкции, как указано в структуре `Initialize`.
 2. `data: u64` — параметр инструкции, который будет передан при вызове инструкции.

 Тело функции устанавливает в поле `data` new_account` предоставленный аргумент `data`, 
 а затем печатает сообщение в журналы программы.

- Макрос `#[derive(Accounts)]` используется для определения структуры, 
  которая определяет учетные записи, необходимые для конкретной инструкции, 
  где каждое поле представляет отдельную учетную запись.

 Типы полей (например, `Signer<'info>`) и ограничения (например, `#[account(mut)]`) 
 используются Anchor для автоматической обработки общих проверок безопасности, 
 связанных с проверкой учетной записи.

  ```rs
  #[derive(Accounts)]
  pub struct Initialize<'info> {
      #[account(init, payer = signer, space = 8 + 8)]
      pub new_account: Account<'info, NewAccount>,
      #[account(mut)]
      pub signer: Signer<'info>,
      pub system_program: Program<'info, System>,
  }
  ```

- Макрос `#[account]` используется для определения структуры, которая представляет 
  структуру данных учетной записи, созданной и принадлежащей программе.

  ```rs
  #[account]
  pub struct NewAccount {
    data: u64
  }
  ```

</details>

### Программа сборки и развертывания

Чтобы собрать программу, просто запустите `build` в терминале.

```shell filename="Terminal"
build
```

Обратите внимание, что адрес в `declare_id!()` был обновлен. 
Это сетевой адрес вашей программы.

<details>
{<summary>Output</summary>}

```shell filename="Terminal"
$ build
Building...
Build successful. Completed in 1.46s.
```

</details>

После сборки программы запустите «deploy» в терминале, 
чтобы развернуть программу в сети (по умолчанию devnet). 
Чтобы развернуть программу, SOL должен быть выделен 
для учетной записи в цепочке, в которой хранится программа.

Перед развертыванием убедитесь, что у вас достаточно SOL. 
Вы можете получить devnet SOL, запустив «solana airdrop 5» 
в терминале Playground или используя [веб-сборщик](https://faucet.solana.com/).

```shell filename="Terminal"
deploy
```

<details>
{<summary>Output</summary>}

```shell filename="Terminal"
$ deploy
Deploying... This could take a while depending on the program size and network conditions.
Warning: 1 transaction not confirmed, retrying...
Deployment successful. Completed in 19s.
```

</details>

Альтернативно вы также можете использовать кнопки «Создать» и «Развернуть» на левой панели.

![Build and Deploy](/assets/docs/intro/quickstart/pg-build-deploy.png)

После развертывания программы вы можете вызывать ее инструкции.

### Тестовая программа

В стартовый код включен тестовый файл, найденный в `tests/anchor.test.ts`. 
Этот файл демонстрирует, как вызвать инструкцию инициализации 
стартовой программы со стороны клиента.

```ts filename="anchor.test.ts"
// No imports needed: web3, anchor, pg and more are globally available

describe("Test", () => {
  it("initialize", async () => {
    // Создайте пару ключей для новой учетной записи.
    const newAccountKp = new web3.Keypair();

    // Отправить транзакцию
    const data = new BN(42);
    const txHash = await pg.program.methods
      .initialize(data)
      .accounts({
        newAccount: newAccountKp.publicKey,
        signer: pg.wallet.publicKey,
        systemProgram: web3.SystemProgram.programId,
      })
      .signers([newAccountKp])
      .rpc();
    console.log(`Use 'solana confirm -v ${txHash}' to see the logs`);

    // Подтвердить транзакцию
    await pg.connection.confirmTransaction(txHash);

    // Получить созданную учетную запись
    const newAccount = await pg.program.account.newAccount.fetch(
      newAccountKp.publicKey,
    );

    console.log("On-chain data is:", newAccount.data.toString());

    // Проверьте, равны ли данные в цепочке локальным 'data'.
    assert(data.eq(newAccount.data));
  });
});
```

Чтобы запустить тестовый файл после развертывания программы, запустите `test` в терминале.

```shell filename="Terminal"
test
```

Вы должны увидеть выходные данные, указывающие, что тест пройден успешно.

<details>
{<summary>Output</summary>}

```shell filename="Terminal"
$ test
Running tests...
  hello_anchor.test.ts:
  hello_anchor
    Use 'solana confirm -v 3TewJtiUz1EgtT88pLJHvKFzqrzDNuHVi8CfD2mWmHEBAaMfC5NAaHdmr19qQYfTiBace6XUmADvR4Qrhe8gH5uc' to see the logs
    On-chain data is: 42
    ✔ initialize (961ms)
  1 passing (963ms)
```

</details>

Вы также можете использовать кнопку `Test` на левой боковой панели.

![Run Test](/assets/docs/intro/quickstart/pg-test.png)


Затем вы можете просмотреть журналы транзакций, выполнив команду `solana confirm -v` 
и указав хэш транзакции (подпись) из результатов теста:

```shell filename="Terminal"
solana confirm -v [TxHash]
```

Например:

```shell filename="Terminal"
solana confirm -v 3TewJtiUz1EgtT88pLJHvKFzqrzDNuHVi8CfD2mWmHEBAaMfC5NAaHdmr19qQYfTiBace6XUmADvR4Qrhe8gH5uc
```

<details>
{<summary>Output</summary>}

```shell filename="Terminal" {29-35}
$ solana confirm -v 3TewJtiUz1EgtT88pLJHvKFzqrzDNuHVi8CfD2mWmHEBAaMfC5NAaHdmr19qQYfTiBace6XUmADvR4Qrhe8gH5uc
RPC URL: https://api.devnet.solana.com
Default Signer: Playground Wallet
Commitment: confirmed

Transaction executed in slot 308150984:
  Block Time: 2024-06-25T12:52:05-05:00
  Version: legacy
  Recent Blockhash: 7AnZvY37nMhCybTyVXJ1umcfHSZGbngnm4GZx6jNRTNH
  Signature 0: 3TewJtiUz1EgtT88pLJHvKFzqrzDNuHVi8CfD2mWmHEBAaMfC5NAaHdmr19qQYfTiBace6XUmADvR4Qrhe8gH5uc
  Signature 1: 3TrRbqeMYFCkjsxdPExxBkLAi9SB2pNUyg87ryBaTHzzYtGjbsAz9udfT9AkrjSo1ZjByJgJHBAdRVVTZv6B87PQ
  Account 0: srw- 3z9vL1zjN6qyAFHhHQdWYRTFAcy69pJydkZmSFBKHg1R (fee payer)
  Account 1: srw- c7yy8zdP8oeZ2ewbSb8WWY2yWjDpg3B43jk3478Nv7J
  Account 2: -r-- 11111111111111111111111111111111
  Account 3: -r-x 2VvQ11q8xrn5tkPNyeraRsPaATdiPx8weLAD8aD4dn2r
  Instruction 0
    Program:   2VvQ11q8xrn5tkPNyeraRsPaATdiPx8weLAD8aD4dn2r (3)
    Account 0: c7yy8zdP8oeZ2ewbSb8WWY2yWjDpg3B43jk3478Nv7J (1)
    Account 1: 3z9vL1zjN6qyAFHhHQdWYRTFAcy69pJydkZmSFBKHg1R (0)
    Account 2: 11111111111111111111111111111111 (2)
    Data: [175, 175, 109, 31, 13, 152, 155, 237, 42, 0, 0, 0, 0, 0, 0, 0]
  Status: Ok
    Fee: ◎0.00001
    Account 0 balance: ◎5.47001376 -> ◎5.46900152
    Account 1 balance: ◎0 -> ◎0.00100224
    Account 2 balance: ◎0.000000001
    Account 3 balance: ◎0.00139896
  Log Messages:
    Program 2VvQ11q8xrn5tkPNyeraRsPaATdiPx8weLAD8aD4dn2r invoke [1]
    Program log: Instruction: Initialize
    Program 11111111111111111111111111111111 invoke [2]
    Program 11111111111111111111111111111111 success
    Program log: Changed data to: 42!
    Program 2VvQ11q8xrn5tkPNyeraRsPaATdiPx8weLAD8aD4dn2r consumed 5661 of 200000 compute units
    Program 2VvQ11q8xrn5tkPNyeraRsPaATdiPx8weLAD8aD4dn2r success

Confirmed
```

</details>

Кроме того, вы можете просмотреть детали транзакции на
[SolanaFM](https://solana.fm/) или
[Solana Explorer](https://explorer.solana.com/?cluster=devnet) 
путем поиска подписи транзакции (хеша).

<Callout>
  Напоминание о необходимости обновить кластерное (сетевое) соединение 
  в используемом вами проводнике для соответствия Solana Playground. 
  Кластером Solana Playground по умолчанию является devnet.
</Callout>

### Закрыть программу

Наконец, SOL, выделенный для программы в цепочке, 
можно полностью восстановить, закрыв программу.

Вы можете закрыть программу, выполнив следующую команду 
и указав адрес программы, найденный в `declare_id!()`:

```shell filename="Terminal"
solana program close [ProgramID]
```

Например:

```shell filename="Terminal"
solana program close 2VvQ11q8xrn5tkPNyeraRsPaATdiPx8weLAD8aD4dn2r
```

<details>
{<summary>Output</summary>}

```shell filename="Terminal"
$ solana program close 2VvQ11q8xrn5tkPNyeraRsPaATdiPx8weLAD8aD4dn2r
Closed Program Id 2VvQ11q8xrn5tkPNyeraRsPaATdiPx8weLAD8aD4dn2r, 2.79511512 SOL reclaimed
```

</details>

<details>
{<summary>Explanation</summary>}

Только авторизация обновления программы может закрыть ее. 
Права на обновление задаются при развертывании программы, 
и это единственная учетная запись, имеющая разрешение 
на изменение или закрытие программы. Если право на обновление отозвано, 
программа становится неизменяемой и ее невозможно закрыть или обновить.

При развертывании программ на Solana Playground ваш кошелек 
Playground является органом обновления для всех ваших программ.

</details>

Поздравляем! Вы только что создали и развернули 
свою первую программу Solana с использованием 
платформы Anchor!

</Steps>

## Производный адрес программы

В этом разделе мы рассмотрим, как создать базовую программу CRUD 
(создание, чтение, обновление, удаление). Программа сохранит 
сообщение пользователя, используя в качестве адреса учетной записи адрес, 
полученный программой (PDA).

Цель этого раздела — провести вас через этапы создания и тестирования 
программы Solana с использованием платформы Anchor и продемонстрировать, 
как использовать КПК в программе. Более подробную информацию 
можно найти на странице [Производный адрес программ](/docs/core/pda).

Для справки, вот [окончательный код](https://beta.solpg.io/668304cfcffcf4b13384d20a) 
после заполнения разделов PDA и CPI.

<Steps>

### Стартовый код

Начните с открытия этой 
[ссылки на игровую площадку Solana] (https://beta.solpg.io/66734b7bcffcf4b13384d1ad) 
со стартовым кодом. Затем нажмите кнопку «Импортировать», 
после чего программа будет добавлена ​​в список проектов на Solana Playground.

![Import](/assets/docs/intro/quickstart/pg-import.png)

В файле `lib.rs` вы найдете программу, оснащенную инструкциями 
`create`, `update` и `delete`, которые мы реализуем на следующих шагах.

```rs filename="lib.rs"
use anchor_lang::prelude::*;

declare_id!("8KPzbM2Cwn4Yjak7QYAEH9wyoQh86NcBicaLuzPaejdw");

#[program]
pub mod pda {
    use super::*;

    pub fn create(_ctx: Context<Create>) -> Result<()> {
        Ok(())
    }

    pub fn update(_ctx: Context<Update>) -> Result<()> {
        Ok(())
    }

    pub fn delete(_ctx: Context<Delete>) -> Result<()> {
        Ok(())
    }
}

#[derive(Accounts)]
pub struct Create {}

#[derive(Accounts)]
pub struct Update {}

#[derive(Accounts)]
pub struct Delete {}

#[account]
pub struct MessageAccount {}
```

Прежде чем мы начнем, запустите `build` в терминале Playground, 
чтобы проверить успешность сборки стартовой программы.

```shell filename="Terminal"
build
```

<details>
{<summary>Output</summary>}

```shell filename="Terminal"
$ build
Building...
Build successful. Completed in 3.50s.
```

</details>

### Определить тип учетной записи сообщения

Сначала давайте определим структуру учетной записи сообщения, 
которую создаст наша программа. Это данные, 
которые мы будем хранить в учетной записи, созданной программой.

В `lib.rs` обновите структуру `MessageAccount` следующим образом:

```rs filename="lib.rs"
#[account]
pub struct MessageAccount {
    pub user: Pubkey,
    pub message: String,
    pub bump: u8,
}
```

<details>
{<summary>Diff</summary>}

```diff
- #[account]
- pub struct MessageAccount {}

+ #[account]
+ pub struct MessageAccount {
+    pub user: Pubkey,
+    pub message: String,
+    pub bump: u8,
+ }
```

</details>

<details>
{<summary>Explanation</summary>}

Макрос `#[account]` в программе Anchor используется для аннотирования структур, 
которые представляют данные учетной записи (тип данных для хранения 
в поле данных AccountInfo).

В этом примере мы определяем структуру `MessageAccount` для хранения сообщения, 
созданного пользователями и содержащего три поля:

- `user`: публичный ключ, представляющий пользователя, создавшего учетную запись сообщения.
- `message`: строка, содержащая сообщение пользователя.
- `bump`: u8, хранящий начальное число "bump", используемое при получении 
  программного адреса (PDA). Сохранение этого значения экономит вычислительные ресурсы, 
  устраняя необходимость его повторного получения для каждого использования 
  в последующих инструкциях.
- `user` — публичный ключ, представляющий пользователя, создавшего учетную запись сообщения.
- `message` — строка, содержащая сообщение пользователя.
- `bump` — u8, хранящий [начальное число "bump"](/docs/core/pda#canonical-bump), 
  используемое при получении программного адреса (PDA). Сохранение этого значения 
  экономит вычислительные ресурсы, устраняя необходимость его повторного получения 
  для каждого использования в последующих инструкциях. При создании учетной записи 
  данные `MessageAccount` будут сериализованы и сохранены в поле данных новой учетной записи.

Позже, при чтении из учетной записи, эти данные можно десериализовать обратно 
в тип данных `MessageAccount`. Процесс создания и чтения данных аккаунта 
будет продемонстрирован в разделе тестирования.

</details>

Соберите программу еще раз, запустив `build` в терминале.

```shell filename="Terminal"
build
```

Мы определили, как будет выглядеть наша учетная запись сообщений. 
Далее реализуем инструкции программы.

### Реализация инструкции создания

Теперь давайте реализуем инструкцию create для создания и инициализации
 `Аккаунт сообщения`.

Начните с определения учетных записей, необходимых для инструкции, 
обновив структуру Create следующим образом:

```rs filename="lib.rs"
#[derive(Accounts)]
#[instruction(message: String)]
pub struct Create<'info> {
    #[account(mut)]
    pub user: Signer<'info>,

    #[account(
        init,
        seeds = [b"message", user.key().as_ref()],
        bump,
        payer = user,
        space = 8 + 32 + 4 + message.len() + 1
    )]
    pub message_account: Account<'info, MessageAccount>,
    pub system_program: Program<'info, System>,
}
```

<details>
{<summary>Diff</summary>}

```diff
- #[derive(Accounts)]
- pub struct Create {}

+ #[derive(Accounts)]
+ #[instruction(message: String)]
+ pub struct Create<'info> {
+     #[account(mut)]
+     pub user: Signer<'info>,
+
+     #[account(
+         init,
+         seeds = [b"message", user.key().as_ref()],
+         bump,
+         payer = user,
+         space = 8 + 32 + 4 + message.len() + 1
+     )]
+     pub message_account: Account<'info, MessageAccount>,
+     pub system_program: Program<'info, System>,
+ }
```

</details>

<details>
{<summary>Explanation</summary>}

Макрос `#[derive(Accounts)]` в программе Anchor используется 
для аннотирования структур, которые представляют список учетных записей, 
требуемых инструкцией, где каждое поле в структуре является учетной записью.

Каждая учетная запись (поле) в структуре помечается типом учетной записи 
(например, `Signer<'info>`) и может быть дополнительно помечена ограничениями 
(например, `#[account(mut)]`). Тип учетной записи вместе с ограничениями 
учетной записи используются для проверки безопасности учетных записей, 
передаваемых в инструкцию.

Именование каждого поля предназначено только для нашего понимания 
и не влияет на проверку учетной записи, однако рекомендуется использовать 
описательные имена учетных записей.

---

Структура `Create` определяет учетные записи, необходимые для инструкции `create`.

1. `user: Signer<'info>`

 - Представляет пользователя, создающего учетную запись сообщения.
 - Помечен как изменяемый (`#[account(mut)]`), поскольку он платит 
   за новую учетную запись.
 - Для подтверждения транзакции необходимо быть подписантом, 
   так как лампорты списываются со счета.

2. `message_account: Account<'info, MessageAccount>`

 - Новая учетная запись, созданная для хранения сообщения пользователя.
 - `init` - ограничение указывает, что учетная запись будет создана в инструкции
 - `seeds` и `bump` - ограничения указывают, что адрес учетной записи 
   является адресом, полученным программой (PDA).
 - `payer = user` указывает учетную запись, оплачивающую создание 
   новой учетной записи.
 - `space` указывает количество байтов, выделенных для поля данных 
   новой учетной записи.

3. `system_program: Program<'info, System>`

 - Требуется для создания новых учетных записей
 - Внутри ограничение `init` вызывает системную программу 
   для создания новой учетной записи, выделенной с указанным `пространством`, 
   и переназначает владельца программы текущей программе.
     
---

Аннотация `#[instruction(message: String)]` позволяет структуре `Create` 
получить доступ к параметру `message` из инструкции `create`.

---

Ограничения `seeds` и `bump` используются вместе, чтобы указать, 
что адрес учетной записи является адресом, полученным программой (PDA).

```rs filename="lib.rs"
seeds = [b"message", user.key().as_ref()],
bump,
```

The `seeds` constraint defines the optional inputs used to derive the PDA.

- `b"message"` - A hardcoded string as the first seed.
- `user.key().as_ref()` - The public key of the `user` account as the second
  seed.

The `bump` constraint tells Anchor to automatically find and use the correct
bump seed. Anchor will use the `seeds` and `bump` to derive the PDA.

---

The `space` calculation (8 + 32 + 4 + message.len() + 1) allocates space for
`MessageAccount` data type:

- Anchor Account discriminator (identifier): 8 bytes
- User Address (Pubkey): 32 bytes
- User Message (String): 4 bytes for length + variable message length
- PDA Bump seed (u8): 1 byte

Ограничение `seeds` определяет дополнительные входные данные, 
используемые для получения PDA.

- `b"message"` — жестко запрограммированная строка в качестве первого начального числа.
- `user.key().as_ref()` — открытый ключ учетной записи `user` 
  в качестве второго начального числа.

Ограничение `bump` сообщает Anchor автоматически найти и использовать 
правильное начальное значение `bump`. Anchor будет использовать `seeds` 
и `bump` для получения PDA.

---

Вычисление `space` (8 + 32 + 4 + message.len() + 1) выделяет пространство для типа данных `MessageAccount`:

- Дискриминатор (идентификатор) Account - привязки учетной записи: 8 байт.
- Адрес пользователя (Pubkey): 32 байта.
- Сообщение пользователя (строка): длина 4 байта + переменная длина сообщения.
- Начальное значение PDA Bump (u8): 1 байт

```rs filename="lib.rs"
#[account]
pub struct MessageAccount {
    pub user: Pubkey,
    pub message: String,
    pub bump: u8,
}
```

Для всех учетных записей, созданных с помощью программы Anchor, требуется 8 байтов 
для дискриминатора учетной записи, который представляет собой идентификатор 
типа учетной записи, который автоматически генерируется при создании учетной записи.

Типу String требуется 4 байта для хранения длины строки, а оставшаяся длина — 
это фактические данные.

</details>

Затем реализуйте бизнес-логику для инструкции `create`, обновив 
функцию `create` следующим образом:

```rs filename="lib.rs"
pub fn create(ctx: Context<Create>, message: String) -> Result<()> {
    msg!("Create Message: {}", message);
    let account_data = &mut ctx.accounts.message_account;
    account_data.user = ctx.accounts.user.key();
    account_data.message = message;
    account_data.bump = ctx.bumps.message_account;
    Ok(())
}
```

<details>
{<summary>Diff</summary>}

```diff
- pub fn create(_ctx: Context<Create>) -> Result<()> {
-     Ok(())
- }

+ pub fn create(ctx: Context<Create>, message: String) -> Result<()> {
+     msg!("Create Message: {}", message);
+     let account_data = &mut ctx.accounts.message_account;
+     account_data.user = ctx.accounts.user.key();
+     account_data.message = message;
+     account_data.bump = ctx.bumps.message_account;
+     Ok(())
+ }
```

</details>

<details>
{<summary>Explanation</summary>}

The `create` function implements the logic for initializing a new message
account's data. It takes two parameters:

1. `ctx: Context<Create>` — обеспечивает доступ к учетным записям, 
   указанным в структуре `Create`.
2. `message: String` — сообщение пользователя, которое нужно сохранить.

Затем тело функции выполняет следующую логику:

1. Распечатайте сообщение в журналы программы, используя макрос `msg!()`.

   ```rs
   msg!("Create Message: {}", message);
   ```

2. Инициализация данных учетной записи:

 - Доступ к `message_account` из контекста.

   ```rs
   let account_data = &mut ctx.accounts.message_account;
   ```

   - Устанавливает в поле `user` открытый ключ учетной записи `user`.

   ```rs
   account_data.user = ctx.accounts.user.key();
   ```

   - Устанавливает в поле `message` значение `message` из аргумента функции.

   ```rs
   account_data.message = message;
   ```

   - Устанавливает значение `bump`, используемое для получения PDA, 
     полученное из `ctx.bumps.message_account`.

   ```rs
   account_data.bump = ctx.bumps.message_account;
   ```

</details>

Пересоберите программу.

```shell filename="Terminal"
build
```

### Внедрить инструкцию по обновлению

Затем выполните инструкцию `update`, чтобы обновить `MessageAccount` новым сообщением.

Как и прежде, первым шагом является указание учетных записей, 
требуемых для инструкции `update`.

Обновите структуру `Update`, указав следующее:

```rs filename="lib.rs"
#[derive(Accounts)]
#[instruction(message: String)]
pub struct Update<'info> {
    #[account(mut)]
    pub user: Signer<'info>,

    #[account(
        mut,
        seeds = [b"message", user.key().as_ref()],
        bump = message_account.bump,
        realloc = 8 + 32 + 4 + message.len() + 1,
        realloc::payer = user,
        realloc::zero = true,
    )]
    pub message_account: Account<'info, MessageAccount>,
    pub system_program: Program<'info, System>,
}
```

<details>
{<summary>Diff</summary>}

```diff
- #[derive(Accounts)]
- pub struct Update {}

+ #[derive(Accounts)]
+ #[instruction(message: String)]
+ pub struct Update<'info> {
+     #[account(mut)]
+     pub user: Signer<'info>,
+
+     #[account(
+         mut,
+         seeds = [b"message", user.key().as_ref()],
+         bump = message_account.bump,
+         realloc = 8 + 32 + 4 + message.len() + 1,
+         realloc::payer = user,
+         realloc::zero = true,
+     )]
+     pub message_account: Account<'info, MessageAccount>,
+     pub system_program: Program<'info, System>,
+ }
```

</details>

<details>
{<summary>Explanation</summary>}

Структура `Update` определяет учетные записи,
необходимые для инструкции `update`.

1. `user: Signer<'info>`

 - Представляет пользователя, обновляющего учетную запись сообщения.
 - Помечено как изменяемое (`#[account(mut)]`), так как при необходимости
   может потребоваться дополнительное место для `message_account`.
 - Должен быть подписантом, чтобы одобрить транзакцию

2. `message_account: Account<'info, MessageAccount>`

 - Существующая учетная запись, в которой хранится сообщение пользователя, которое будет обновлено.
 - `mut` - ограничение указывает, что данные этой учетной записи будут изменены.
 - `realloc` - ограничение позволяет изменять размер данных учетной записи.
 - `seeds` и`bump` - ограничения гарантируют, что учетная запись является правильным PDA.

3. `system_program: Program<'info, System>`
 - Требуется для потенциального перераспределения пространства учетной записи.
 - `realloc` - ограничение  вызывает системную программу 
   для настройки размера данных учетной записи.

---

Обратите внимание, что ограничение `bump = message_account.bump` использует 
начальное значение bump seed, хранящееся в `mesesage_account`, вместо того, 
чтобы Anchor пересчитывал его.

---

`#[instruction(message: String)]` - аннотация позволяет структуре `Update` 
получить доступ к параметру `message` из инструкции `update`.

</details>

Затем реализуйте логику инструкции `update`.

```rs filename="lib.rs"
pub fn update(ctx: Context<Update>, message: String) -> Result<()> {
    msg!("Update Message: {}", message);
    let account_data = &mut ctx.accounts.message_account;
    account_data.message = message;
    Ok(())
}
```

<details>
{<summary>Diff</summary>}

```diff
- pub fn update(_ctx: Context<Update>) -> Result<()> {
-     Ok(())
- }

+ pub fn update(ctx: Context<Update>, message: String) -> Result<()> {
+     msg!("Update Message: {}", message);
+     let account_data = &mut ctx.accounts.message_account;
+     account_data.message = message;
+     Ok(())
+ }
```

</details>

<details>
{<summary>Explanation</summary>}

Функция `update` реализует логику изменения существующей учетной записи сообщения. 
Он принимает два параметра:

1. `ctx: Context<Update>` — обеспечивает доступ к учетным записям, 
   указанным в структуре `Update`.
2. `message: String` — Новое сообщение взамен существующего.

Тогда тело функции:

1. печатаут сообщение в логи (журналы) программы, используя макрос `msg!()`.

2. Обновляет данные учетной записи (Account Data):
 - Доступ к `message_account` из контекста.
 - Устанавливает в поле `message` новое `message` из аргумента функции.

</details>

Пересобрать программу

```shell filename="Terminal"
build
```

### Выполнить инструкцию удаления

Затем выполните инструкцию `delete`, чтобы закрыть `MessageAccount`.

Обновите структуру `Delete` следующим образом:

```rs filename="lib.rs"
#[derive(Accounts)]
pub struct Delete<'info> {
    #[account(mut)]
    pub user: Signer<'info>,

    #[account(
        mut,
        seeds = [b"message", user.key().as_ref()],
        bump = message_account.bump,
        close= user,
    )]
    pub message_account: Account<'info, MessageAccount>,
}
```

<details>
{<summary>Diff</summary>}

```diff
- #[derive(Accounts)]
- pub struct Delete {}

+ #[derive(Accounts)]
+ pub struct Delete<'info> {
+     #[account(mut)]
+     pub user: Signer<'info>,
+
+     #[account(
+         mut,
+         seeds = [b"message", user.key().as_ref()],
+         bump = message_account.bump,
+         close = user,
+     )]
+     pub message_account: Account<'info, MessageAccount>,
+ }
```

</details>

<details>
{<summary>Explanation</summary>}

Структура `Delete` определяет учетные записи, необходимые для инструкции `delete`:

1. `user: Signer<'info>`

 - Представляет пользователя, закрывающего учетную запись сообщения.
 - Помечен как изменяемый (`#[account(mut)]`), так как он будет получать 
   лампорты из закрытого аккаунта.
 - Должен быть подписывающим лицом, чтобы гарантировать, что только правильный пользователь 
   может закрыть свою учетную запись сообщения.

2. `message_account: Account<'info, MessageAccount>`

 - Счет (Account) закрывается
 - `mut` - ограничение указывает, что эта учетная запись будет изменена
 - `seeds` и`bump` - ограничения гарантируют, что учетная запись является правильным PDA.
 - `close = user` - ограничение  указывает, что эта учетная запись будет закрыта, 
   а ее лампорты перенесены в учетную запись `user`.

</details>

Затем реализуйте логику инструкции `update`.

```rs filename="lib.rs"
pub fn delete(_ctx: Context<Delete>) -> Result<()> {
    msg!("Delete Message");
    Ok(())
}
```

<details>
{<summary>Diff</summary>}

```diff
- pub fn delete(_ctx: Context<Delete>) -> Result<()> {
-     Ok(())
- }

+ pub fn delete(_ctx: Context<Delete>) -> Result<()> {
+     msg!("Delete Message");
+     Ok(())
+ }
```

</details>

<details>
{<summary>Explanation</summary>}

Функция delete принимает один параметр:

1. `_ctx: Context<Delete>` — обеспечивает доступ к учетным записям, 
указанным в структуре `Delete`. Синтаксис `_ctx` указывает, 
что мы не будем использовать контекст в теле функции.

Тело функции печатает сообщение в логи (журналы) программы только с помощью макроса `msg!()`. 
Функция не требует какой-либо дополнительной логики, поскольку 
фактическое закрытие учетной записи обрабатывается ограничением `close` в структуре `Delete`.

</details>

Пересоберите программу.

```shell filename="Terminal"
build
```

### Развернуть программу

Базовая программа CRUD завершена. Разверните программу, запустив `deploy`
в терминале игровой площадки.

```shell filename="Terminal"
deploy
```

<details>
{<summary>Output</summary>}

```bash
$ deploy
Deploying... This could take a while depending on the program size and network conditions.
Deployment successful. Completed in 17s.
```

</details>

### Настроить тестовый файл

В стартовый код также включен тестовый файл `anchor.test.ts`.

```ts filename="anchor.test.ts"
import { PublicKey } from "@solana/web3.js";

describe("pda", () => {
  it("Create Message Account", async () => {});

  it("Update Message Account", async () => {});

  it("Delete Message Account", async () => {});
});
```

Добавьте приведенный ниже код внутри `describe`, но перед разделами `it`.

```ts filename="anchor.test.ts"
const program = pg.program;
const wallet = pg.wallet;

const [messagePda, messageBump] = PublicKey.findProgramAddressSync(
  [Buffer.from("message"), wallet.publicKey.toBuffer()],
  program.programId,
);
```

<details>
{<summary>Diff</summary>}

```diff
  import { PublicKey } from "@solana/web3.js";

  describe("pda", () => {
+    const program = pg.program;
+    const wallet = pg.wallet;
+
+    const [messagePda, messageBump] = PublicKey.findProgramAddressSync(
+      [Buffer.from("message"), wallet.publicKey.toBuffer()],
+      program.programId
+    );

    it("Create Message Account", async () => {});

    it("Update Message Account", async () => {});

    it("Delete Message Account", async () => {});
  });
```

</details>

<details>
{<summary>Explanation</summary>}

В этом разделе мы просто настраиваем тестовый файл.

Solana Playground удаляет некоторые шаблонные настройки, где `pg.program` 
позволяет нам получить доступ к клиентской библиотеке для взаимодействия с программой, 
а `pg.wallet` — это ваш игровой кошелек.

```ts filename="anchor.test.ts"
const program = pg.program;
const wallet = pg.wallet;
```

В рамках настройки мы получаем учетную запись сообщений PDA. 
Это демонстрирует, как получить КПК в Javascript, используя начальные значения, 
указанные в программе.

```ts filename="anchor.test.ts"
const [messagePda, messageBump] = PublicKey.findProgramAddressSync(
  [Buffer.from("message"), wallet.publicKey.toBuffer()],
  program.programId,
);
```

</details>

Запустите тестовый файл, запустив `test` в терминале Playground, 
чтобы убедиться, что файл работает должным образом. 
Мы реализуем тесты на следующих шагах.

```shell filename="Terminal"
test
```

<details>
{<summary>Output</summary>}

```bash
$ test
Running tests...
  anchor.test.ts:
  pda
    ✔ Create Message Account
    ✔ Update Message Account
    ✔ Delete Message Account
  3 passing (4ms)
```

</details>

### Invoke Create Instruction

Обновите первый тест следующим образом:

```ts filename="anchor.test.ts"
it("Create Message Account", async () => {
  const message = "Hello, World!";
  const transactionSignature = await program.methods
    .create(message)
    .accounts({
      messageAccount: messagePda,
    })
    .rpc({ commitment: "confirmed" });

  const messageAccount = await program.account.messageAccount.fetch(
    messagePda,
    "confirmed",
  );

  console.log(JSON.stringify(messageAccount, null, 2));
  console.log(
    "Transaction Signature:",
    `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
  );
});
```

<details>
{<summary>Diff</summary>}

```diff
- it("Create Message Account", async () => {});

+ it("Create Message Account", async () => {
+   const message = "Hello, World!";
+   const transactionSignature = await program.methods
+     .create(message)
+     .accounts({
+       messageAccount: messagePda,
+     })
+     .rpc({ commitment: "confirmed" });
+
+   const messageAccount = await program.account.messageAccount.fetch(
+     messagePda,
+     "confirmed"
+   );
+
+   console.log(JSON.stringify(messageAccount, null, 2));
+   console.log(
+     "Transaction Signature:",
+     `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`
+   );
+ });
```

</details>

<details>
{<summary>Explanation</summary>}

Сначала мы отправляем транзакцию, которая вызывает инструкцию create, 
передавая "Hello, World!" как сообщение.

```ts filename="anchor.test.ts"
const message = "Hello, World!";
const transactionSignature = await program.methods
  .create(message)
  .accounts({
    messageAccount: messagePda,
  })
  .rpc({ commitment: "confirmed" });
```

После отправки транзакции и создания учетной записи 
мы извлекаем учетную запись, используя ее адрес (`messagePda`).

```ts filename="anchor.test.ts"
const messageAccount = await program.account.messageAccount.fetch(
  messagePda,
  "confirmed",
);
```

Наконец, мы регистрируем данные учетной записи и ссылку для просмотра 
деталей транзакции.

```ts filename="anchor.test.ts"
console.log(JSON.stringify(messageAccount, null, 2));
console.log(
  "Transaction Signature:",
  `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
);
```

</details>

### Вызов инструкции обновления

Обновите второй тест следующим образом:

```ts filename="anchor.test.ts"
it("Update Message Account", async () => {
  const message = "Hello, Solana!";
  const transactionSignature = await program.methods
    .update(message)
    .accounts({
      messageAccount: messagePda,
    })
    .rpc({ commitment: "confirmed" });

  const messageAccount = await program.account.messageAccount.fetch(
    messagePda,
    "confirmed",
  );

  console.log(JSON.stringify(messageAccount, null, 2));
  console.log(
    "Transaction Signature:",
    `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
  );
});
```

<details>
{<summary>Diff</summary>}

```diff
- it("Update Message Account", async () => {});

+ it("Update Message Account", async () => {
+   const message = "Hello, Solana!";
+   const transactionSignature = await program.methods
+     .update(message)
+     .accounts({
+       messageAccount: messagePda,
+     })
+     .rpc({ commitment: "confirmed" });
+
+   const messageAccount = await program.account.messageAccount.fetch(
+     messagePda,
+     "confirmed"
+   );
+
+   console.log(JSON.stringify(messageAccount, null, 2));
+   console.log(
+     "Transaction Signature:",
+     `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`
+   );
+ });
```

</details>

<details>
{<summary>Explanation</summary>}

Сначала мы отправляем транзакцию, которая вызывает инструкцию обновления, 
передавая "Привет, Солана!" как новое сообщение.

```ts filename="anchor.test.ts"
const message = "Hello, Solana!";
const transactionSignature = await program.methods
  .update(message)
  .accounts({
    messageAccount: messagePda,
  })
  .rpc({ commitment: "confirmed" });
```

После отправки транзакции и обновления учетной записи мы извлекаем учетную запись, 
используя ее адрес (`messagePda`).

```ts filename="anchor.test.ts"
const messageAccount = await program.account.messageAccount.fetch(
  messagePda,
  "confirmed",
);
```

Наконец, мы регистрируем данные учетной записи и ссылку для просмотра деталей транзакции.

```ts filename="anchor.test.ts"
console.log(JSON.stringify(messageAccount, null, 2));
console.log(
  "Transaction Signature:",
  `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
);
```

</details>

### Вызов инструкции удаления

Обновите третий тест следующим образом:

```ts filename="anchor.test.ts"
it("Delete Message Account", async () => {
  const transactionSignature = await program.methods
    .delete()
    .accounts({
      messageAccount: messagePda,
    })
    .rpc({ commitment: "confirmed" });

  const messageAccount = await program.account.messageAccount.fetchNullable(
    messagePda,
    "confirmed",
  );

  console.log("Expect Null:", JSON.stringify(messageAccount, null, 2));
  console.log(
    "Transaction Signature:",
    `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
  );
});
```

<details>
{<summary>Diff</summary>}

```diff
- it("Delete Message Account", async () => {});

+ it("Delete Message Account", async () => {
+   const transactionSignature = await program.methods
+     .delete()
+     .accounts({
+       messageAccount: messagePda,
+     })
+     .rpc({ commitment: "confirmed" });
+
+   const messageAccount = await program.account.messageAccount.fetchNullable(
+     messagePda,
+     "confirmed"
+   );
+
+   console.log("Expect Null:", JSON.stringify(messageAccount, null, 2));
+   console.log(
+     "Transaction Signature:",
+     `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`
+   );
+ });
```

</details>

<details>
{<summary>Explanation</summary>}

Сначала мы отправляем транзакцию, которая вызывает инструкцию `delete` 
для закрытия учетной записи сообщения.

```ts filename="anchor.test.ts"
const transactionSignature = await program.methods
  .delete()
  .accounts({
    messageAccount: messagePda,
  })
  .rpc({ commitment: "confirmed" });
```

Как только транзакция отправлена ​​и учетная запись закрыта, 
мы пытаемся получить учетную запись, используя ее адрес (`messagePda`), 
используя `fetchNullable`, поскольку мы ожидаем, что возвращаемое значение 
будет нулевым, поскольку учетная запись закрыта.

```ts filename="anchor.test.ts"
const messageAccount = await program.account.messageAccount.fetchNullable(
  messagePda,
  "confirmed",
);
```

Наконец, мы регистрируем данные учетной записи и ссылку для просмотра 
деталей транзакции, где данные учетной записи должны быть зарегистрированы 
как нулевые.

```ts filename="anchor.test.ts"
console.log(JSON.stringify(messageAccount, null, 2));
console.log(
  "Transaction Signature:",
  `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
);
```

</details>

### Запустить тест

После настройки тестов запустите тестовый файл, запустив `test` 
в терминале Playground.

```shell filename="Terminal"
test
```

<details>
{<summary>Output</summary>}

```bash
$ test
Running tests...
  anchor.test.ts:
  pda
    {
  "user": "3z9vL1zjN6qyAFHhHQdWYRTFAcy69pJydkZmSFBKHg1R",
  "message": "Hello, World!",
  "bump": 254
}
    Transaction Signature: https://solana.fm/tx/5oBT4jEdUR6CRYsFNGoqvyMBTRDvFqRWTAAmCGM9rEvYRBWy3B2bkb6GVFpVPKBnkr714UCFUurBSDKSa7nLHo8e?cluster=devnet-solana
    ✔ Create Message Account (1025ms)
    {
  "user": "3z9vL1zjN6qyAFHhHQdWYRTFAcy69pJydkZmSFBKHg1R",
  "message": "Hello, Solana!",
  "bump": 254
}
    Transaction Signature: https://solana.fm/tx/42veGAsQjHbJP1SxWBGcfYF7EdRN9X7bACNv23NSZNe4U7w2dmaYgSv8UUWXYzwgJPoNHejhtWdKZModHiMaTWYK?cluster=devnet-solana
    ✔ Update Message Account (713ms)
    Expect Null: null
    Transaction Signature: https://solana.fm/tx/Sseog2i2X7uDEn2DyDMMJKVHeZEzmuhnqUwicwGhnGhstZo8URNwUZgED8o6HANiojJkfQbhXVbGNLdhsFtWrd6?cluster=devnet-solana
    ✔ Delete Message Account (812ms)
  3 passing (3s)
```

</details>

</Steps>

## Межпрограммный вызов

В этом разделе мы обновим нашу существующую программу CRUD, 
включив в нее межпрограммные вызовы (CPI). Мы модифицируем программу 
для передачи SOL между учетными записями в инструкциях `update` и `delete`, 
демонстрируя, как взаимодействовать с другими программами 
(в данном случае с системной программой) изнутри нашей программы.

Цель этого раздела — пройти через процесс реализации CPI в программе Solana 
с использованием платформы Anchor, основываясь на концепциях PDA, 
которые мы рассмотрели в предыдущем разделе. Более подробную информацию 
можно найти на странице [Межпрограммный вызов](/docs/core/cpi).

<Steps>

### Изменить инструкцию по обновлению

Сначала мы реализуем простой механизм `pay-to-update`, 
изменив структуру `Update` и функцию `update`.

Начните с обновления файла `lib.rs`, чтобы включить в него элементы 
из модуля `system_program`.

```rs filename="lib.rs"
use anchor_lang::system_program::{transfer, Transfer};
```

<details>
{<summary>Diff</summary>}

```diff
  use anchor_lang::prelude::*;
+ use anchor_lang::system_program::{transfer, Transfer};
```

</details>

Затем обновите структуру `Update`, включив в нее дополнительную учетную 
запись `vault_account`. Эта учетная запись, контролируемая нашей программой, 
будет получать SOL от пользователя, когда он обновит свою учетную запись сообщений.

```rs filename="lib.rs"
#[account(
    mut,
    seeds = [b"vault", user.key().as_ref()],
    bump,
)]
pub vault_account: SystemAccount<'info>,
```

<details>
{<summary>Diff</summary>}

```diff
#[derive(Accounts)]
#[instruction(message: String)]
pub struct Update<'info> {
    #[account(mut)]
    pub user: Signer<'info>,

+   #[account(
+       mut,
+       seeds = [b"vault", user.key().as_ref()],
+       bump,
+   )]
+   pub vault_account: SystemAccount<'info>,
    #[account(
        mut,
        seeds = [b"message", user.key().as_ref()],
        bump = message_account.bump,
        realloc = 8 + 32 + 4 + message.len() + 1,
        realloc::payer = user,
        realloc::zero = true,
    )]
    pub message_account: Account<'info, MessageAccount>,
    pub system_program: Program<'info, System>,
}
```

</details>

<details>
{<summary>Explanation</summary>}

Мы добавляем новую учетную запись с именем `vault_account` в нашу структуру `Update`. 
Эта учетная запись служит программно-управляемым `vault` ('"хранилищем"), 
которое будет получать SOL от пользователей, когда они обновляют свои сообщения.

Используя PDA для vault ("хранилища"), мы создаем управляемую программой учетную запись, 
уникальную для каждого пользователя, что позволяет нам управлять средствами пользователей 
в рамках логики нашей программы.

---

Key aspects of the `vault_account`:

- The address of the account is a PDA derived using seeds
  `[b"vault", user.key().as_ref()]`
- As a PDA, it has no private key, so only our program can "sign" for the
  address when performing CPIs
- As a `SystemAccount` type, it's owned by the System Program like regular
  wallet accounts

This setup allows our program to:

- Generate unique, deterministic addresses for each user's "vault"
- Control funds without needing a private key to sign for transactions.

In the `delete` instruction, we'll demonstrate how our program can "sign" for
this PDA in a CPI.

</details>

Next, implement the CPI logic in the `update` instruction to transfer 0.001 SOL
from the user's account to the vault account.

```rs filename="lib.rs"
let transfer_accounts = Transfer {
    from: ctx.accounts.user.to_account_info(),
    to: ctx.accounts.vault_account.to_account_info(),
};
let cpi_context = CpiContext::new(
    ctx.accounts.system_program.to_account_info(),
    transfer_accounts,
);
transfer(cpi_context, 1_000_000)?;
```

<details>
{<summary>Diff</summary>}

```diff
    pub fn update(ctx: Context<Update>, message: String) -> Result<()> {
        msg!("Update Message: {}", message);
        let account_data = &mut ctx.accounts.message_account;
        account_data.message = message;

+       let transfer_accounts = Transfer {
+           from: ctx.accounts.user.to_account_info(),
+           to: ctx.accounts.vault_account.to_account_info(),
+       };
+       let cpi_context = CpiContext::new(
+           ctx.accounts.system_program.to_account_info(),
+           transfer_accounts,
+       );
+       transfer(cpi_context, 1_000_000)?;
        Ok(())
    }
```

</details>

<details>
{<summary>Explanation</summary>}

In the `update` instruction, we implement a Cross Program Invocation (CPI) to
invoke the System Program's `transfer` instruction. This demonstrates how to
perform a CPI from within our program, enabling the composability of Solana
programs.

The `Transfer` struct specifies the required accounts for the System Program's
transfer instruction:

- `from` - The user's account (source of funds)
- `to` - The vault account (destination of funds)

  ```rs filename="lib.rs"
  let transfer_accounts = Transfer {
      from: ctx.accounts.user.to_account_info(),
      to: ctx.accounts.vault_account.to_account_info(),
  };
  ```

The `CpiContext` specifies:

- The program to be invoked (System Program)
- The accounts required in the CPI (defined in the `Transfer` struct)

  ```rs filename="lib.rs"
  let cpi_context = CpiContext::new(
      ctx.accounts.system_program.to_account_info(),
      transfer_accounts,
  );
  ```

The `transfer` function then invokes the transfer instruction on the System
Program, passing in the:

- The `cpi_context` (program and accounts)
- The `amount` to transfer (1,000,000 lamports, equivalent to 0.001 SOL)

  ```rs filename="lib.rs"
  transfer(cpi_context, 1_000_000)?;
  ```

---

The setup for a CPI matches how client-side instructions are built, where we
specify the program, accounts, and instruction data for a particular instruction
to invoke. When our program's `update` instruction is invoked, it internally
invokes the System Program's transfer instruction.

</details>

Rebuild the program.

```shell filename="Terminal"
build
```

### Modify Delete Instruction

We'll now implement a "refund on delete" mechanism by modifying the `Delete`
struct and `delete` function.

First, update the `Delete` struct to include the `vault_account`. This allows us
to transfer any SOL in the vault back to the user when they close their message
account.

```rs filename="lib.rs"
#[account(
    mut,
    seeds = [b"vault", user.key().as_ref()],
    bump,
)]
pub vault_account: SystemAccount<'info>,
```

Also add the `system_program` as the CPI for the transfer requires invoking the
System Program.

```rs filename="lib.rs"
pub system_program: Program<'info, System>,
```

<details>
{<summary>Diff</summary>}

```diff
#[derive(Accounts)]
pub struct Delete<'info> {
    #[account(mut)]
    pub user: Signer<'info>,

+   #[account(
+       mut,
+       seeds = [b"vault", user.key().as_ref()],
+       bump,
+   )]
+   pub vault_account: SystemAccount<'info>,
    #[account(
        mut,
        seeds = [b"message", user.key().as_ref()],
        bump = message_account.bump,
        close= user,
    )]
    pub message_account: Account<'info, MessageAccount>,
+   pub system_program: Program<'info, System>,
}
```

</details>

<details>
{<summary>Explanation</summary>}

The `vault_account` uses the same PDA derivation as in the Update struct.

Add the `vault_account` to the Delete struct enables our program to access the
user's vault account during the delete instruction to transfer any accumulated
SOL back to the user.

</details>

Next, implement the CPI logic in the `delete` instruction to transfer SOL from
the vault account back to the user's account.

```rs filename="lib.rs"
let user_key = ctx.accounts.user.key();
let signer_seeds: &[&[&[u8]]] =
    &[&[b"vault", user_key.as_ref(), &[ctx.bumps.vault_account]]];

let transfer_accounts = Transfer {
    from: ctx.accounts.vault_account.to_account_info(),
    to: ctx.accounts.user.to_account_info(),
};
let cpi_context = CpiContext::new(
    ctx.accounts.system_program.to_account_info(),
    transfer_accounts,
).with_signer(signer_seeds);
transfer(cpi_context, ctx.accounts.vault_account.lamports())?;
```

Note that we updated `_ctx: Context<Delete>` to `ctx: Context<Delete>` as we'll
be using the context in the body of the function.

<details>
{<summary>Diff</summary>}

```diff
-    pub fn delete(_ctx: Context<Delete>) -> Result<()> {
+    pub fn delete(ctx: Context<Delete>) -> Result<()> {
         msg!("Delete Message");

+        let user_key = ctx.accounts.user.key();
+        let signer_seeds: &[&[&[u8]]] =
+            &[&[b"vault", user_key.as_ref(), &[ctx.bumps.vault_account]]];
+
+        let transfer_accounts = Transfer {
+            from: ctx.accounts.vault_account.to_account_info(),
+            to: ctx.accounts.user.to_account_info(),
+        };
+        let cpi_context = CpiContext::new(
+            ctx.accounts.system_program.to_account_info(),
+            transfer_accounts,
+        ).with_signer(signer_seeds);
+        transfer(cpi_context, ctx.accounts.vault_account.lamports())?;
         Ok(())
     }

```

</details>

<details>
{<summary>Explanation</summary>}

In the delete instruction, we implement another Cross Program Invocation (CPI)
to invoke the System Program's transfer instruction. This CPI demonstrates how
to make a transfer that requires a Program Derived Address (PDA) signer.

First, we define the signer seeds for the vault PDA:

```rs filename="lib.rs"
let user_key = ctx.accounts.user.key();
let signer_seeds: &[&[&[u8]]] =
    &[&[b"vault", user_key.as_ref(), &[ctx.bumps.vault_account]]];
```

The `Transfer` struct specifies the required accounts for the System Program's
transfer instruction:

- from: The vault account (source of funds)
- to: The user's account (destination of funds)

  ```rs filename="lib.rs"
  let transfer_accounts = Transfer {
      from: ctx.accounts.vault_account.to_account_info(),
      to: ctx.accounts.user.to_account_info(),
  };
  ```

The `CpiContext` specifies:

- The program to be invoked (System Program)
- The accounts involved in the transfer (defined in the Transfer struct)
- The signer seeds for the PDA

  ```rs filename="lib.rs"
  let cpi_context = CpiContext::new(
      ctx.accounts.system_program.to_account_info(),
      transfer_accounts,
  ).with_signer(signer_seeds);
  ```

The transfer function then invokes the transfer instruction on the System
Program, passing:

- The `cpi_context` (program, accounts, and PDA signer)
- The amount to transfer (the entire balance of the vault account)

  ```rs filename="lib.rs"
  transfer(cpi_context, ctx.accounts.vault_account.lamports())?;
  ```

This CPI implementation demonstrates how programs can utilize PDAs to manage
funds. When our program's delete instruction is invoked, it internally calls the
System Program's transfer instruction, signing for the PDA to authorize the
transfer of all funds from the vault back to the user.

</details>

Rebuild the program.

```shell filename="Terminal"
build
```

### Redeploy Program

After making these changes, we need to redeploy our updated program. This
ensures that our modified program is available for testing. On Solana, updating
a program simply requires deploying the compiled program at the same program ID.

```shell filename="Terminal"
deploy
```

<details>
{<summary>Output</summary>}

```bash
$ deploy
Deploying... This could take a while depending on the program size and network conditions.
Deployment successful. Completed in 17s.
```

</details>

<details>
{<summary>Explanation</summary>}

Only the upgrade authority of the program can update it. The upgrade authority
is set when the program is deployed, and it's the only account with permission
to modify or close the program. If the upgrade authority is revoked, then the
program becomes immutable and can never be closed or upgraded.

When deploying programs on Solana Playground, your Playground wallet is the
upgrade authority for all your programs.

</details>

### Update Test File

Next, we'll update our `anchor.test.ts` file to include the new vault account in
our instructions. This requires deriving the vault PDA and including it in our
update and delete instruction calls.

#### Derive Vault PDA

First, add the vault PDA derivation:

```ts filename="anchor.test.ts"
const [vaultPda, vaultBump] = PublicKey.findProgramAddressSync(
  [Buffer.from("vault"), wallet.publicKey.toBuffer()],
  program.programId,
);
```

<details>
{<summary>Diff</summary>}

```diff
describe("pda", () => {
  const program = pg.program;
  const wallet = pg.wallet;

  const [messagePda, messageBump] = PublicKey.findProgramAddressSync(
    [Buffer.from("message"), wallet.publicKey.toBuffer()],
    program.programId
  );

+  const [vaultPda, vaultBump] = PublicKey.findProgramAddressSync(
+    [Buffer.from("vault"), wallet.publicKey.toBuffer()],
+    program.programId
+  );

  // ...tests
  });
```

</details>

#### Modify Update Test

Then, update the update instruction to include the `vaultAccount`.

```ts filename="anchor.test.ts"  {5}
const transactionSignature = await program.methods
  .update(message)
  .accounts({
    messageAccount: messagePda,
    vaultAccount: vaultPda,
  })
  .rpc({ commitment: "confirmed" });
```

<details>
{<summary>Diff</summary>}

```diff
    const transactionSignature = await program.methods
      .update(message)
      .accounts({
        messageAccount: messagePda,
+       vaultAccount: vaultPda,
      })
      .rpc({ commitment: "confirmed" });
```

</details>

#### Modify Delete Test

Then, update the delete instruction to include the `vaultAccount`.

```ts filename="anchor.test.ts"  {5}
const transactionSignature = await program.methods
  .delete()
  .accounts({
    messageAccount: messagePda,
    vaultAccount: vaultPda,
  })
  .rpc({ commitment: "confirmed" });
```

<details>
{<summary>Diff</summary>}

```diff
    const transactionSignature = await program.methods
      .delete()
      .accounts({
        messageAccount: messagePda,
+       vaultAccount: vaultPda,
      })
      .rpc({ commitment: "confirmed" });
```

</details>

### Rerun Test

After making these changes, run the tests to ensure everything is working as
expected:

```shell filename="Terminal"
test
```

<details>
{<summary>Output</summary>}

```bash
$ test
Running tests...
  anchor.test.ts:
  pda
    {
  "user": "3z9vL1zjN6qyAFHhHQdWYRTFAcy69pJydkZmSFBKHg1R",
  "message": "Hello, World!",
  "bump": 254
}
    Transaction Signature: https://solana.fm/tx/qGsYb87mUUjeyh7Ha7r9VXkACw32HxVBujo2NUxqHiUc8qxRMFB7kdH2D4JyYtPBx171ddS91VyVrFXypgYaKUr?cluster=devnet-solana
    ✔ Create Message Account (842ms)
    {
  "user": "3z9vL1zjN6qyAFHhHQdWYRTFAcy69pJydkZmSFBKHg1R",
  "message": "Hello, Solana!",
  "bump": 254
}
    Transaction Signature: https://solana.fm/tx/3KCDnNSfDDfmSy8kpiSrJsGGkzgxx2mt18KejuV2vmJjeyenkSoEfs2ghUQ6cMoYYgd9Qax9CbnYRcvF2zzumNt8?cluster=devnet-solana
    ✔ Update Message Account (946ms)
    Expect Null: null
    Transaction Signature: https://solana.fm/tx/3M7Z7Mea3TtQc6m9z386B9QuEgvLKxD999mt2RyVtJ26FgaAzV1QA5mxox3eXie3bpBkNpDQ4mEANr3trVHCWMC2?cluster=devnet-solana
    ✔ Delete Message Account (859ms)
  3 passing (3s)
```

</details>

You can then inspect the SolanFM links to view the transaction details, where
you’ll find the CPIs for the transfer instructions within the update and delete
instructions.

![Update CPI](/assets/docs/intro/quickstart/cpi-update.png)

![Delete CPI](/assets/docs/intro/quickstart/cpi-delete.png)

If you encounter any errors, you can reference the
[final code](https://beta.solpg.io/668304cfcffcf4b13384d20a).

</Steps>

## Next Steps

You've completed the Solana Quickstart guide! You've learned about accounts,
transactions, PDAs, CPIs, and deployed your own programs.

Visit the [Core Concepts](/docs/core/accounts) pages for more comprehensive
explanations of the topics covered in this guide.

Additional learning resources can be found on the
[Developer Resources](/developers) page.

### Explore More Examples

If you prefer learning by example, check out the
[Program Examples Repository](https://github.com/solana-developers/program-examples)
for a variety of example programs.

Solana Playground offers a convenient feature allowing you to import or view
projects using their GitHub links. For example, open this
[Solana Playground link](https://beta.solpg.io/https://github.com/solana-developers/program-examples/tree/main/basics/hello-solana/anchor)
to view the Anchor project from this
[Github repo](https://github.com/solana-developers/program-examples/tree/main/basics/hello-solana/anchor).

Click the `Import` button and enter a project name to add it to your list of
projects in Solana Playground. Once a project is imported, all changes are
automatically saved and persisted within the Playground environment.

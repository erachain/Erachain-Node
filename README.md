# Start Node documentation

## Java
Use Java 1.8 64 JRE or SDK from https://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html#javasejdk

## Start Options
see \z_bath_examples\readme.txt

**-nonet**  
No use Network

**-testnet**  
-testnet[=GENESIS_TIMESTAMP]  
-testnet=[XXXX] - Start in TestNET mode and set Genesis Block Timestamp (in millis).  
-testnet - set genesis Timestamp = current Date and `-nonet` is ON and use 9065 port  
-testnet=demo - set genesis Timestamp = DEMO chain on 9066 port  
-testnet=0 - set current NTP genesis Timestamp on port 9065  
For start generation of blocks need more than 5 accounts on all nodes or in Your wallet is used '-testnet'.  

**-cli**  
start as Command Line Interpretator. You may send RPC commands.

**-pass=PASSWORD**  
start forging. Keys will read once from walletKeys file on start.

**-peers=PEER1,PEER2,...**  
example: -peers=34.12.211.156,35.99.02.177

**-seed=ACCOUNTS_NUMBER:SEED:PASSWORD** 
if SEED lenght < 30 - It will made new SEED  
example for restore: -seed=3:AXR1wqktmgNYVnpR5uYwBh5v6K6kFb2XH1KYjwDroKcy:1  
example for auto make wallet keys: -seed=3:New:1  

**-backup**

**-nogui**  
Start without GUI

**-nousewallet**  
Not use secret wallet Keys - speed up - not forging

**-nodatawallet**  
Not use data Wallet - speed up

**-opi**  
Only Protocol Indexing. This option speed up. Blockexplorer, API and RPC wil not work.

**-nocalculated**  
Not store calculated transactions in DB. Make speed up

**-dbschain=rocksdb | mapdb | fast**  
Select DataBase for dataChain. rocksdb - RocksDB or mapdb - MapDB or fast - it si complex DB for fast speed (default).
Default: `mapdb`. `fast` and `rocksdb` is experimental now.
	
## Bath files
Examples for batch (command) files for start with forging and loop restart see in `\z_bath_examples`

Copy bath-file to root folder and run it.

Example for Windows:  
start "erachain" java -jar erachain.jar -pass=1 -seed=3:AXRJwqktmgNYVnpR5uYwBh5v6K6kFb2XH1KYjwDroKcy:1

# RPC script commands
Set `ON` in Node Settings (File -> Settings -> Main) for RPC Server. Set Access Permission for local.
Use console in Node GUI (Network Browse -> Console) or -cli mode or CURL or web-browser for send commands to RPC port.

Type `help` in Console for help on RPC commands.

> If GUI is ON than commands will rise prompt window for password.

## Multi Send
Multi send scrip for send asset for many addresses or persons filtered by some parameters.
This command will run as test for calculate FEE and total AMOUNT by default. For run real send set parameter `test=false`.  

In console type:
`GET r_send/multisend/...`
In web-browser type:
`http://127.0.0.1:9048/r_send/multisend/...`

**Parameters:**  


     * @param fromAddress     my address in Wallet
     * @param assetKey        asset Key that send
     * @param forAssetKey     asset key of holders test
     * @param amount          absolute amount to send
     * @param onlyPerson      Default: false. Use only person accounts
     * @param gender          Filter by gender. -1 = all, 0 - man, 1 - woman. Default: -1.
     * @param position        test balance position. 1 - Own, 2 - Credit, 3 - Hold, 4 - Spend, 5 - Other
     * @param greatEqual      test balance is great or equal
     * @param selfPay         if set - pay to self address too. Default = true
     * @param test            default - true. test=false - real send
     * @param feePow
     * @param activeAfterStr  timestamp after that is filter - yyyy-MM-dd hh:mm or timestamp(sec)
     * @param activeBeforeStr timestamp before that is filter - yyyy-MM-dd hh:mm or timestamp(sec) activetypetx
     * @param activeTypeTX    if set - test only that type transactions
     * @param koeff           koefficient for amount in balance position of forAssetKey
     * @param title
     * @param password


Example:
  
     * GET r_send/multisend/7LSN788zgesVYwvMhaUbaJ11oRGjWYagNA/1036/2?amount=0.001&title=probe-multi&onlyperson=true&activeafter=1577712486&password=123
     * GET r_send/multisend/7LSN788zgesVYwvMhaUbaJ11oRGjWYagNA/1069/1036?amount=0.001&title=probe-multi&onlyperson=true&activeafter=2018-01-01 00:00&activebefore=2019-01-01 00:00&greatequal=0&activetypetx=24&password=1
     * GET r_send/multisend/7A94JWgdnNPZtbmbphhpMQdseHpKCxbrZ1/1/2?amount=0.001&title=probe-multi&onlyperson=true&gender=0&password=1

**Transaction types:**

    // ISSUE ITEMS
    ISSUE_ASSET_TRANSACTION = 21;
    ISSUE_IMPRINT_TRANSACTION = 22;
    ISSUE_TEMPLATE_TRANSACTION = 23;
    ISSUE_PERSON_TRANSACTION = 24;
    ISSUE_STATUS_TRANSACTION = 25;
    ISSUE_UNION_TRANSACTION = 26;
    ISSUE_STATEMENT_TRANSACTION = 27;
    ISSUE_POLL_TRANSACTION = 28;
    // SEND ASSET
    SEND_ASSET_TRANSACTION = 31;
    // OTHER
    SIGN_NOTE_TRANSACTION = 35;
    CERTIFY_PUB_KEYS_TRANSACTION = 36;
    SET_STATUS_TO_ITEM_TRANSACTION = 37;
    SET_UNION_TO_ITEM_TRANSACTION = 38;
    SET_UNION_STATUS_TO_ITEM_TRANSACTION = 39;
    // confirm other transactions
    VOUCH_TRANSACTION = 40;
    // HASHES
    HASHES_RECORD = 41;
    // exchange of assets
    CREATE_ORDER_TRANSACTION = 50;
    CANCEL_ORDER_TRANSACTION = 51;
    // voting
    CREATE_POLL_TRANSACTION = 61;
    VOTE_ON_POLL_TRANSACTION = 62;
    VOTE_ON_ITEM_POLL_TRANSACTION = 63;
    RELEASE_PACK = 70;

    CALCULATED_TRANSACTION = 100;


## Если кошелек пустой (Мои Счета)
Если в ноде в ГУИ в закладе Мои Счета не все счета появились или вообще пусто то надо:  
1. в настройках задать Минимльное чило пиров = 0 - чтобы нода не начинала синхронизироваться  
2. забанить в Обзор сети -> Дополнительная Информация все пиры с которых идет синхронизация  
3. в этом случае в Мои Счета кнопка Создать Счет и Синхронизировать Кошелек станут активными  
4. нажать или Добавить Счет или Синхронизировать Кошелек - при синхронизации подтянутся все счета, а при добавить счет добавятся несозданные счета  
5. в настройках опять поставить 10 пиров минимально  
6. подключиться к пирам (правая мышка на пирах в Дополнительная Информация) или перегрузить прогу  

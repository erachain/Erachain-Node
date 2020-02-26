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


# StakeWars-Event-Guide-Episode-III
Event Info: Stake Wars is a program to familiarize the community with what it means to be a NEAR validator, and gives the community early access to a Chunk-only producer

Time: July 13 — September 9, 2022

Audience: Anyone can join at any time during the event period, but please join as soon as possible to take advantage of the program’s benefits

I.Challenge 001.md: Configuration requirements:

![image](https://user-images.githubusercontent.com/108244458/181517189-502d6f2f-d3f6-4761-830f-f705338f7764.png)


i bought 1 private VPS on Contabo for a reasonable price.

![image](https://user-images.githubusercontent.com/108244458/181517294-ee8f9bfd-56c3-45a7-b2ac-7861dcebb172.png)


Create a Wallet:

Create your own Shardnet wallet: https://wallet.shardnet.near.org/

![image](https://user-images.githubusercontent.com/108244458/181517360-238024b8-9b68-437f-b395-d5e418f71791.png)

!Note: The NEAR tokens given away are not real.

Updating Linux machines:

sudo apt update && sudo apt upgrade -y

![image](https://user-images.githubusercontent.com/108244458/181517476-bcd7bd5b-edb9-481f-816c-26e4cfde90cf.png)

Install developer tools, Node.js, and npm:

curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash —

apt install build-essential nodejs

PATH=”$PATH”

![image](https://user-images.githubusercontent.com/108244458/181517552-3504216d-34cf-44e2-ab9f-e92903b52690.png)

Test:

Install NEAR-CLI:

sudo npm install -g near-cli

![image](https://user-images.githubusercontent.com/108244458/181517629-b6df79b7-1476-4e53-8214-9ea4516ca973.png)

Now NEAR-CLI is installed!

We will set up Shardnet environment for Chunk-only producer:Create Shardnet Environment

export NEAR_ENV=shardnet

![image](https://user-images.githubusercontent.com/108244458/181517701-a56d26b9-b565-4b00-8e9e-994b383048db.png)

You can check other NEAR CLI Command Guides here: https://github.com/near/stakewars-iii/blob/main/challenges/001.md

II.Challenge 002.md

Make sure your VPS’s CPU is supported

lscpu | grep -P ‘(?=.*avx )(?=.*sse4.2 )(?=.*cx16 )(?=.*popcnt )’ > /dev/null
&& echo “Supported”
|| echo “Not supported”

![image](https://user-images.githubusercontent.com/108244458/181517770-ef7b8bb2-be49-4787-87f8-93a82eb8d00c.png)

Install developer tools:

sudo apt install -y git binutils-dev libcurl4-openssl-dev zlib1g-dev libdw-dev libiberty-dev cmake gcc g++ python docker.io protobuf-compiler libssl-dev pkg-config clang llvm cargo

![image](https://user-images.githubusercontent.com/108244458/181517833-1a1d8280-9569-403c-a377-bc6f5aa7485d.png)

Install Python pip:

sudo apt install python3-pip

![image](https://user-images.githubusercontent.com/108244458/181517902-f474dc89-28e7-45f5-ae51-f7d2c7712c53.png)

![image](https://user-images.githubusercontent.com/108244458/181517941-1d2ddeb3-4089-4ea9-8982-57098c240305.png)

Configure:
USER_BASE_BIN=$(python3 -m site — user-base)/bin

export PATH=”$USER_BASE_BIN:$PATH”

Install Building Env:

sudo apt install clang build-essential make

Install Rust & Cargo:


curl — proto ‘=https’ — tlsv1.2 -sSf https://sh.rustup.rs | sh

![image](https://user-images.githubusercontent.com/108244458/181518108-128b301d-19bc-489a-8d2b-cd1da2de2ac7.png)

Hit “y” and enter

![image](https://user-images.githubusercontent.com/108244458/181518180-2b7230dd-c3e5-4550-92df-c2c9a34c2037.png)

Press 1 and ENTER

Then:

source $HOME/.cargo/env

Clone nearcore from Github:

git clone https://github.com/near/nearcore cd nearcore git fetch


![image](https://user-images.githubusercontent.com/108244458/181518258-2f31a805-26aa-4cae-86fe-05e4e2935e68.png)


Checkout to the commit needed. Please refer to the latest commit in Event Discord

git checkout

For now it will be

git checkout 8448ad1eb

![image](https://user-images.githubusercontent.com/108244458/181518318-2a31e536-8e67-405f-b6bc-e50821620da6.png)

Then execute this command:

cargo build -p neard — release — features shardnet

![image](https://user-images.githubusercontent.com/108244458/181518388-93bfe899-00f7-4b21-85c3-0b77ae8ddd18.png)

It will take 7–10 mins to complete.

Then:Initialize working directory


./target/release/neard — home ~/.near init — chain-id shardnet — download-genesis

![image](https://user-images.githubusercontent.com/108244458/181518440-422f2e63-5595-403c-9d62-01b5f7ac9e55.png)

It will create a directory structure and will create config.json, node_key.json and genesis.json on the network you passed.

Replace config.json

rm ~/.near/config.json wget -O ~/.near/config.json https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/config.json

![image](https://user-images.githubusercontent.com/108244458/181518518-2e60e5a2-5f60-4f99-bf1b-55e5061d34f8.png)

Get the latest snapshot (this part will be skipped because after Hardfork on shardnet during 2022–07–18, it’s not required)

Install AWS CLI

sudo apt-get install awscli -y

![image](https://user-images.githubusercontent.com/108244458/181518580-5f94a7fb-b729-4eca-97c4-c047dc6bf8e2.png)

Next We activating the node as validator

A full access key needs to be installed locally to be able to sign transactions via NEAR-CLI.

Wallet Login:

Execute command:

Near Login Copy the link to the browser: (Drag and highlight and right click to copy — don’t press Ctrl+c):

![image](https://user-images.githubusercontent.com/108244458/181518670-c55cb258-edcb-4476-8611-f82eb7119810.png)

2.Then hit “next” and “connect”

Then enter your accountID and hit “confirm”

![image](https://user-images.githubusercontent.com/108244458/181518730-5a750dfc-2377-4b4f-b457-ec9912393edd.png)

3.Then the browser will appear as follows:

![image](https://user-images.githubusercontent.com/108244458/181518802-ff5dd70e-6e8c-48af-ac51-02a89d7388ee.png)

Go back and enter your Shardnet wallet address and you will get the message:

![image](https://user-images.githubusercontent.com/108244458/181518869-af36d377-c526-4afa-8dbe-f18eb6f4b2eb.png)

when successfully, we are good to go

Check the validator_key.json

cat ~/.near/validator_key.json

Replace the <pool_id> with your pool ID, for example

near generate-key hoang51993.factory.shardnet.near

Generate validator_key file from your wallet:

cp ~/.near-credentials/shardnet/YOUR_WALLET.json ~/.near/validator_key.json

Edit validator_key: Change “private_key” to “secret_key”:

nano $HOME/.near/validator_key.json

{ “account_id”:”xx.factory.shardnet.near”,” public_key”:”ed25519:47KQrU**************************************”, “secret_key”:”ed25519:***************************************************************************************” }

Use this command:

sudo nano ~/.near/validator_key.json

![image](https://user-images.githubusercontent.com/108244458/181518951-a35f20d1-da29-438d-a2f1-2ac22b608bb1.png)

Then hit Ctrl + O to write out and hit Ctrl +X to exit

Now setup System Command

sudo nano /etc/systemd/system/neard.service

and paste this

[Unit] Description=NEARd Daemon Service

[Service] Type=simple User= #Group=near WorkingDirectory=/home//.near ExecStart=/home//nearcore/target/release/neard run Restart=on-failure RestartSec=30 KillSignal=SIGINT TimeoutStopSec=45 KillMode=mixed

[Install] WantedBy=multi-user.target

Note: Change USER to your paths

![image](https://user-images.githubusercontent.com/108244458/181519011-182670e7-c76b-469d-8708-a163146814bc.png)

Then Ctrl +O to save and Ctrl +X to exit

Check Logs:

journalctl -n 100 -f -u neard

![image](https://user-images.githubusercontent.com/108244458/181519060-998b5d53-efcb-4b1c-a1cf-0e2416edafca.png)

To get out hit Ctrl + C

Make log output in pretty print:

Setup: CCZE

sudo apt install ccze

![image](https://user-images.githubusercontent.com/108244458/181519126-aab9dcc1-8430-475d-92b7-9969fbf45e26.png)

View Logs with color:

journalctl -n 100 -f -u neard | ccze -A

![image](https://user-images.githubusercontent.com/108244458/181519205-3911e22c-feed-4029-a060-96c63f883cc2.png)

To get out hit Ctrl + C

III.Challenge 003.md:

Deploy Staking pool:

near call factory.shardnet.near create_staking_pool ‘{“staking_pool_id”: “”, “owner_id”: “”, “stake_public_key”: “”, “reward_fee_fraction”: {“numerator”: 5, “denominator”: 100}, “code_hash”:”DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ”}’ — accountId=”” — amount=30 — gas=300000000000000

From the example above, you need to replace:

Pool ID: Staking pool name, the factory automatically adds its name to this parameter, creating {pool_id}.{staking_pool_factory} Examples: If pool id is stakewars will create : stakewars.factory.shardnet.near Owner ID: The SHARDNET account (i.e. stakewares.shardnet.near) that will manage the staking pool. Public Key: The public key in your validator_key.json file. 5: The fee the pool will charge (e.g. in this case 5 over 100 is 5% of fees). Account Id: The SHARDNET account deploying and signing the mount tx. Usually the same as the Owner ID. Now check in the explore: https://explorer.shardnet.near.org/nodes/validators
![image](https://user-images.githubusercontent.com/108244458/181519269-b3cb4b58-6505-4203-a12f-08b9a77b9ecb.png)
Congratulation! you are successfully create a Node Validator

Now you can check out some transaction guides here: https://github.com/near/stakewars-iii/blob/main/challenges/003.md#transactions-guide
Other functions that can be used:

Ping
near call <staking_pool_id> ping ‘{}’ — accountId — gas=300000000000000

Balances Total Balance Command:
near view <staking_pool_id> get_account_total_balance ‘{“account_id”: “”}’

Staked Balance
near view <staking_pool_id> get_account_staked_balance ‘{“account_id”: “”}’

Unstaked Balance
near view <staking_pool_id> get_account_unstaked_balance ‘{“account_id”: “”}’

Available for Withdrawal
near view <staking_pool_id> is_account_unstaked_balance_available ‘{“account_id”: “”}’

Pause / Resume Staking
near call <staking_pool_id> pause_staking ‘{}’ — accountId

Resume
near call <staking_pool_id> resume_staking ‘{}’ — accountId

You have now configured your Staking pool:

https://explorer.shardnet.near.org/nodes/validators

IV:Challenge 004.md:

Setup tools for monitoring node status.

We have setup log in challenge 002

Use this command to see log:

journalctl -n 100 -f -u neard | ccze -A

Now we install RPC with this commandsudo apt install curl jq:

sudo apt install curl jq

Common Commands: ####### Check your node version: Command:

curl -s http://127.0.0.1:3030/status | jq .version

####### Check Delegators and Stake Command:

near view .factory.shardnet.near get_accounts '{"from_index": 0, "limit": 10}' --accountId .shardnet.near ####### Check Reason Validator Kicked Command:

curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' 127.0.0.1:3030 | jq -c '.result.prev_epoch_kickout[] | select(.account_id | contains ("<POOL_ID>"))' | jq .reason ####### Check Blocks Produced / Expected Command:

curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' 127.0.0.1:3030 | jq -c '.result.current_validators[] | select(.account_id | contains ("POOL_ID"))'

V:Challenge 005.md:

Deliverables Article doing a step-by-step guide on how to mount a node validator. (GitHub or Medium) Submit the form !(https://docs.google.com/forms/d/e/1FAIpQLScp9JEtpk1Fe2P9XMaS9Gl6kl9gcGVEp3A5vPdEgxkHx3ABjg/viewform) with your article.

VI:Challenge 006.md:

Create Crontab for the server
Create a new scripts folder:

Create a new file on /home/<USER_ID>/scripts/ping.sh

#!/bin/sh

Ping call to renew Proposal added to crontab
export NEAR_ENV=shardnet export LOGS=/home/<USER_ID>/logs export POOLID=<YOUR_POOL_ID> export ACCOUNTID=<YOUR_ACCOUNT_ID>

echo "---" >> $LOGS/all.log date >> $LOGS/all.log near call $POOLID.factory.shardnet.near ping '{}' --accountId $ACCOUNTID.shardnet.near --gas=300000000000000 >> $LOGS/all.log near proposals | grep $POOLID >> $LOGS/all.log near validators current | grep $POOLID >> $LOGS/all.log near validators next | grep $POOLID >> $LOGS/all.log

Create a new crontab, running every 5 minutes:

crontab -e */5 * * * * sh /home/<USER_ID>/scripts/ping.sh List crontab to see it is running:

crontab -l Review your logs

cat home/<USER_ID>/logs/all.log

Ping is done periodically to network. (Every 5 minutes)
















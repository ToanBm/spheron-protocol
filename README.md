# Spheron Protocol
## Deploy Your App on Spheron Protocol
### Step 1: Install Spheron Protocol sphnctl CLI
```Bash
curl -sL1 https://sphnctl.sh | bash
```
```Bash
sphnctl -h
```
### Step 2: Create wallet using the CLI
- Creat a new wallet
```Bash
sphnctl wallet create --name <wallet-name>
```
- Here is an example of how the result will look:
```Bash
Created account xxx:
 path: /Users/mitrasish-personal/.spheron/xxxxxyx.json
 address: 0x5C2432F3cB41927212e46e7224036d78eF3F2A93
 secret: xxxxxxxxxx
 mnemonic: xxxxxx xxxxx xxxx xxxxx xxxxx xxxx xxxxx xxxxx
```
#### - Changing Your Wallet (Option)
- If you need to switch to a different wallet, use the command below, providing the name and the key-secret of the new wallet:
```Bash
sphnctl wallet use --name <wallet-name> --key-secret <key-secret>
```
Example: `sphnctl wallet use --name wallet --key-secret xxxxxxxxxx`

Here is an example of how the result will look:
```Bash
Switched default account to xxx:
	path: /Users/mitrasish-personal/.spheron/acbv.json
	address: 0x2c11A76298A111B8cAAvvvvvv05dc8f0A268ASCS
	passphrase: test
```
- Export the Private Key of Wallet
You can export your private key of the wallets you created in local and import it in metamask:
```Bash
sphnctl wallet private-key
```
### Step 3: Get Some test tokens from the Faucet and ETH from the Faucet
Visit the [Spheron Faucet](https://faucet.spheron.network/)
- First, get some ETH gas tokens on the Spheron chain
- Next, get some USDT tokens for testing deployment
- Check if you got the test ETH and USDT tokens in your wallet:
```Bash
sphnctl wallet balance --token USDT
```
This will show both USDT and ETH balances in your wallet.
### Step 4: Deposit some token to Your Escrow Balance
- Deposit USDT / any other token to the escrow wallet:
```Bash
sphnctl payment deposit --amount 20 --token USDT
```
- Now check if you have a balance in an unlocked state in your wallet:
```Bash
sphnctl wallet balance --token USDT
```
### Step 5: Deploy an app
- Creat file `gpu.yml`
```Bash
cat > gpu.yml <<EOF
---
version: "1.0"
 
services:
  web:
    image: jupyter/minimal-notebook:latest
    expose:
      - port: 8888
        as: 8888
        to:
          - global: true
    env:
      - TEST=test
profiles:
  name: hello-world
  duration: 2min
  mode: provider # or 'fizz' for Fizz Mode
  tier:
    - community
  compute:
    web:
      resources:
        cpu:
          units: 0.5
        memory:
          size: 1Gi
        storage:
          size: 1Gi
  placement:
    westcoast:
      attributes:
        region: us-east
      pricing:
        web:
          token: USDT
          amount: 50
deployment:
  web:
    westcoast:
      profile: web
      count: 1
EOF
```
- Deploy the configuration on Spheron Protocol, run:
```Bash
sphnctl deployment create gpu.yml
```
- Here is an example of how the result will look:
```Bash
Checking ballance for wallet: your-wallet
Validating SDL configuration.
SDL validated.
Sending configuration for provider matching.
Deployment order created: [Tx Hash]
Waiting for providers to bid on the deployment order...
Bid found.
Order matched successfully.
Deployment created using wallet your-wallet
 lid: <your-ID>
 provider: 0x6634d41cccBD1E1576Ed4c6226832521A66bF874
 agreed price: 158747943694
Sending the manifest for deployment…
Deployment manifest sent, waiting for acknowledgment.
Deployment is finished.
```
### Step 6: Access Your Deployment
```Bash
sphnctl deployment get --lid <your-ID>
```
### Step 7: Fetching Deployment Logs
```Bash
sphnctl deployment logs --lid <your-ID>
```
### Step 8: Connect to the deployment shell
```Bash
sphnctl deployment shell web /bin/sh --lid <your-ID> --stdin --tty
```

## Congratulations! Your app is now deployed and accessible. 

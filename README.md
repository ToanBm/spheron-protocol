# Spheron Protocol
## Upgrade-v1.1.1
### 1. Download the `fizzup-v1.0.1.sh` script to your PC.
- In `fizz-node` folder on your VPS, choose upload file `fizzup-v1.1.1.sh`.
```console
cd fizz-node
```
### 2. Give persmissions to script
```console
chmod +x fizzup-v1.1.1.sh
```
### 3. Run Fizz Node Script
```
./fizzup-v1.1.1.sh
```
### 4. Check the logs
```
docker-compose -f ~/.spheron/fizz/docker-compose.yml logs -f
```

## ........ Done! .............................................


## Part 1. Deploy Your App on Spheron Protocol
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
### Congratulations! Your app is now deployed and accessible.
------------------------------------------------------------------------------------------------------------------------
## Part 2. Run Fizz Node
## Hardware Requirement
![image](https://github.com/user-attachments/assets/d9d9f0a7-a2f2-41da-8194-16d6dd4b8a00)

## Register Fizz Node
1. Open Your Browser: Navigate to https://fizz.spheron.network
2. Sign up or log in through Gmail or Github
3. Click on the “Register New Fizz Node” Button and Connect your wallet
![image](https://github.com/user-attachments/assets/2876dc7d-dc59-460c-9a0d-f42ce0ea4343)
4. Select your node's OS, resources, Region, Payment Tokens, and Provider ( I selected highest tier provider )
![image](https://github.com/user-attachments/assets/536c09d7-1af6-4832-9b4c-33b9861fecd6)
![image](https://github.com/user-attachments/assets/2ce43536-0cbd-435a-baf3-9beb0c05c645)
5. Click **“Register Your Fizz Node“**, To complete the registration, you'll need some ETH on the Spheron chain for gas fees. If you don't have any, you can get some from our faucet at https://faucet.spheron.network
![image](https://github.com/user-attachments/assets/afcd4cd4-240d-46aa-a5d8-6d35bdea0741)
## Run the Fizz Node
1. Install Docker
Check version!
```console
docker --version
```
2. In setup page for your registered nod, You should find a link to download the `fizzup.sh` script
![image](https://github.com/user-attachments/assets/3052022b-2a14-42a7-8613-bf6ea5624a08)
3. Download the `fizzup.sh` script to your PC.
- Creat `node folder`
- In `fizz-node` folder on your VPS, choose upload file fizzup.sh.
```console
mkdir fizz-node && cd fizz-node
```
4. Give persmissions to script
```console
chmod +x fizzup.sh
```
5. Run Fizz Node Script
```
./fizzup.sh
```
![image](https://github.com/user-attachments/assets/8c9d5d68-fa8c-42be-96e3-25f9958a0c25)

> You’ll earn more if your node provides higher-tier resources such as a powerful GPU or more CPU cores.

> Fizz Nodes must maintain at least 50% uptime within an ERA (24 hours) to receive rewards

> I've ran this node using CPU-only but you can run with GPU for more rewards

## Check Node health
```
docker compose -f ~/.spheron/fizz/docker-compose.yml logs -f
```
or
```
docker-compose -f ~/.spheron/fizz/docker-compose.yml logs -f
```
![image](https://github.com/user-attachments/assets/654ba484-14a2-4994-9a88-bdc10480b327)
Once you've verified the node is running, return to the setup page on the Spheron Fizz App
1. On the setup page, you'll see a "Check Status" button and a switch to "Automatically check status." Click the "Check Status" button to manually initiate a status check for your Fizz node
2. Alternatively, you can toggle on the "Automatically check status" switch to have the system periodically check your node's status without manual intervention
![image](https://github.com/user-attachments/assets/4c22eeda-92b3-4951-a572-d40bceb7585d)
3. The system will now perform checks to validate if your node is active and correctly configured
The validation process may take a few minutes. During this time, the system verifies your node's connectivity, resource availability, and configuration. Once your node is confirmed active, you will be automatically directed to your Fizz dashboard
![image](https://github.com/user-attachments/assets/a35241fd-841b-4ad6-bd99-36dc1a74970c)
## Claim your NFT in the Dashboard
![Screenshot_371](https://github.com/user-attachments/assets/f4b932eb-1ba4-42aa-837e-8d31b36b67f2)
## Join Discord and Claim your role
Discord: https://discord.gg/spheron-network-745315423783878757
Role: https://guild.xyz/spheronfdn
![image](https://github.com/user-attachments/assets/1ffe2ef2-4acc-49df-bc78-b87d7d041f8e)

## Check your VPS resources (RAM, CPU) with htop
```console
sudo apt install htop
htop
```
![image](https://github.com/user-attachments/assets/f767070a-543a-4a43-a8d0-8150bfbcf487)

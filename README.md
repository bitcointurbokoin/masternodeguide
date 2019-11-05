Bitcoin Turbo Koin Masternode Setup Guide
==========================

## Introduction

This guide is for a single masternode, on a Ubuntu 18.04 64-bit server (VPS) running headless and will be controlled from the wallet on your local computer (Control wallet). The wallet on the the VPS will be referred to as the Remote wallet.

You will need your masternode server details for progressing through this guide including the public IP address.

First the basic requirements:

1. 10,000 BTK
1. A main computer (your everyday computer) – This will run the Bitcoin Turbo Koin Core control wallet, hold your collateral 10,000 BTK and can be opened and closed without affecting the masternode.
1. Masternode Server (VPS Suggested – The wallet daemon that will be on 24/7).
1. A unique IP address for your VPS / Remote wallet.

**For security reasons, you’re are going to need a different IP for each masternode you plan to host.**

## Configuration

**Step 1:** Using the control wallet, enter the debug console `Tools > Debug console` and type the following command:

```
masternode genkey
```

*(This will be the masternode’s privkey variable. We will need this later…)*

**Step 2:** Using the control wallet, enter the following command:

```
getaccountaddress "chooseAnyNameForYourMasternode"
```

**Step 3:** Still in the control wallet, send 10,000 BTK to the wallet address you generated in Step 2. 

Be 100% sure that you entered the address correctly. You can verify this when you paste the address into the **"Pay To:"** field, the label will auto populate with the name you chose. 

Also make sure this is exactly **10,000 BTK**; No less, no more.

**Be absolutely sure the send to address is copied correctly and then check it again. We cannot help you if you send 10,000 BTK to an incorrect address.**

Please allow at least 1 block confirmation to complete before moving on.

**Step 4:** Still in the control wallet, enter the command into the console:

```
masternode outputs
```

*This gets the proof of transaction of sending 10,000 BTK*

**Step 5:** Still on the main computer, go into the BTK data directory:

OS | Path to BTK
------------ | -------------
Windows | `%Appdata%/BTK/`
macOS | `~/Library/Application\ Support/BTK/`
Linux | `~/.btk/`

Find the masternode.conf file, edit it in your favorite text editor and add the following line to it:

```
<Name of Masternode(Use the name you entered earlier for simplicity)> <Unique VPS Public IP address>:41242 <The result of Step 1> <Result of Step 4> <The number after the long line in Step 4>
```

Example:

```
MN1 35.25.120.101:41242 894FPpFdbr7sr6Si4fdsfssjjapuFzAXwEVCrpPJubnrmU6aKzh c8f4865da57a68d0e6ddd84324dfd28cfbe0c901015b973e7331bb8ce018716999 1
```

Substitute with your own values and without the "<>"s.

Lastly, close the control wallet and open again to load the new configuration file.

## VPS Remote Wallet Install

Install the latest version of the Bitcoin Turbo Koin Core wallet onto your masternode. The latest version can be found here: [Bitcoin Turbo Koin Core Releases](https://github.com/bitcointurbokoin/btkblockchain/releases).

**Step 1:** Log in to your VPS:

```
cd ~
```

**Step 2:** From your home directory, download the latest version from the BTK GitHub repository:

```
wget https://github.com/bitcointurbokoin/btkblockchain/releases/download/v2.0/btk-x86_64-linux-gnu.tar.gz
```

Always check the releases page for the latest version and update the URL to reflect the most current version.

**Step 3:** Unzip & Extract:

```
tar -zxvf btk-x86_64-linux-gnu.tar.gz
```

**Step 4:** Go to your Bitcoin Turbo Koin bin directory:

```
cd ~/btk/bin
```

**Step 5:** Note: If this is the first time running the wallet in the VPS, you’ll need to attempt to start the wallet:

```
./btkd -daemon
```

**Step 6:** Stop the daemon after the blockchain downloads:

```
./btk-cli stop
```

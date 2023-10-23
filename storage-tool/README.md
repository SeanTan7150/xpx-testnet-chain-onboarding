# Get Started

The Sirius Storage Tool is a user desktop app to interact with Sirius Storage.

## Download
[Windows](https://files.proximax.io/storage-tool/windows-storage-tool.zip)
[Linux](https://files.proximax.io/storage-tool/linux-storage-tool.tar.xz)

## Installation

### Windows
1. Open `file explorer` and find the `windows-storage-tool.zip` zipped file
2. To unzip the file, double-click the zipped folder to open it. Then, drag or copy the item from the zipped folder to a new location
3. Go to the new location and enter the `windows-storage-tool` folder.
4. Double click on `StorageClientApp.exe` to run it.

**Note**: You may be prompted by Windows that Microsoft Defender SmartScreen is preventing this unrecognized app from Starting.  Click on `More Info` and click on the `Run Anyway` button.

### Ubuntu Linux
1. Open your linux terminal
2. Run the following commands to download and install the storage tool:

```bash
wget https://files.proximax.io/storage-tool/linux-storage-tool.tar.xz
tar -xvf linux-storage-tool.tar.xz
cd linux-storage-tool
./StorageClientApp
```


## Initial set up

1. Enter `Account name` and `Private Key`.  Click on `Generate Key` if you wish to use a new private key.  Please ensure the account has `XPX`.

2. Click on `Save` to continue.

3. Enter the following information for settings:

- REST Server Address: `api-2.testnet2.xpxsirius.io:3000` or `18.142.186.205:3000`
- Replicator Bootstrap Address: `genesis-p2p-2.testnet2.xpxsirius.io:7904` or `54.151.161.246:7904`
- Local UDP Port: `6846` (Default Port)
- Account Name: **Select the Account Name in Step 1**
- Download folder: **Click `Choose Directory` to select the directory you want to download files from drives**
- Fee Multiplier: `15000` (default fee multiplier for *Testnet2*)

4. Click on `Save` to save your configurations.

**Tips**: You may use `nslookup` command to retrieve both REST Server and Replicator Bootstrap addresses.

## Get test-XPX from faucet

1. Open storage tool `Settings` and click on `Copy Account Key` to copy your `Public Key`.

2. Paste your `Public Key` to the empty string and run the code below:

```go
package main

import (
  "fmt"
	"github.com/proximax-storage/go-xpx-chain-sdk/sdk"
)

func main() {
	publicKey := ""
	Address, _ := sdk.NewAddressFromPublicKey(publicKey, sdk.MijinTest)
	fmt.Printf("Address:\t\t%v\n", Address.Address)
	fmt.Printf("NetworkType:\t%v", Address.Type)
}
```

3. Copy your `Public Address` displayed as `40` characters in terminal.

4. Head to [Sirius Faucet](bctestnet2faucet.xpxsirius.io), paste your `Public Address` and click on `Send` to receive test-XPX.

## Create drive

1. Click on `+` in `Drives` tab to add drive.

2. Enter the following information for Create Drive dialog:

- Name: **Enter any name of your choosing**
- Replicator Number: **Enter the number of replicators (`5`)**
- Max Drive Size: **Enter an amount that does not exceed the smallest capacity among the onboarded replicators (`1024`)**
- Local Drive Folder: **Click `Choose Directory` to select the directory you want the local drive to be located**

3. Click on `Confirm` to create drive.

4. Your drive will now appear in the drop-down list of drives as `(creating...)` appended to its name, indicating that it has been ordered, but not created yet.

5. Notification will be received if drive is created successfully.

## Upload files to replicator

1. When the drive is created, your files in local drive will appear in green color at the right half of the window. The right half represents difference between your `Local Drive` and `Replicated Drive`.

2. Click `Apply Changes` to upload files to replicators.

3. Notification will be received if the modification is registered completed.

4. Your files will appear at the left half of the window, indicating that the `Replicated Drive` now contains them.

## Deploy a supercontract

1. After uploading supercontract `(.wasm)` files to replicators, click on `Contracts` tab.

2. Click on `Deployment` tab and enter the following information for deployment:

- Drive: **Select the Drive created**
- Assignee: **Enter the `Public Key` to which the test-XPX is transferred during Supercontract Closure (`AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA`)**
- File: **Enter the name of the main supercontract to be executed first**
- Function: **Enter the name of the function to be executed first**
- Parameters: **Enter the parameters of the function mentioned `(optional)`**
- Execution Call Payment: **Select a limit of `SC` units for one supercontract execution**
- Download Call Payment: **Select a limit of `SM` units for one `SM` synchronization**
- Automatic Executions Number: **Select an amount**
- Automatic Executions File Name: **Enter the name of the auxiliary supercontract for automated executions**
- Automatic Execution Function Name: **Enter the name of the function to be executed if the auxiliary supercontract requirement is met**
- Automatic Execution Call Payment: **Select a limit of `SC` units for one automated supercontract execution**
- Automatic Download Call Payment: **Select a limit of `SM` units for one `SM` synchronization**

3. Click on `Deploy` to deploy supercontract.

**Note**: Function names does not include parentheses. e.g.: Enter `run` instead of `run()`.

**Tips**: One drive can only hold a single contract. You can create multiple drives from the same local folder as long as their cumulative size doesn’t exceed replicator capacity.

## Remove drive

1. Click on `-` in `Drives` tab and click on `Confirm` to remove drive.

2. Your drive will now appear in the drop-down list of drives as `(...deleting)` appended to its name, indicating that it has been ordered, but not closed yet.

3. Notification will be received if drive is removed/closed successfully.

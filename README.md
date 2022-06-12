
# Bedrock Addons Installer
Bedrock Dedicated Server Addon Installer is a node tool used for automatically installing, updating, and uninstalling both addons and packs for the Mojang released bedrock servers.

https://www.minecraft.net/en-us/download/server/bedrock/

For help reach out on discord @ http://discord.BedrockRealms.com

## Standard Users (command line tool)

#### How to Install 
1. Install Node.js 14.1.0+
    - Node is used to execute javascript, which this tool is written in.
    - https://nodejs.org/en/ *(Make sure you click the right version)*
2. Open a terminal or command prompt.
    - On windows, click start & then type cmd. 
3. Type the below command to install the tool. 
    - npm install -g bedrock-addons-installer

#### How to Use
1. Open a terminal or command prompt.
    - on windows, click start & then type cmd
2. Navigate to the folder where your bedrock server is installed. 
    - Example: cd .\Desktop\mcServer\
    - If you need more help it is time to google "how to use command prompt".
3. Run the tool for the first time to create the Bedrock-Addons folder.
    - Type "bedrock-addons-installer" without the quotes. 
4. Copy all of your .mcpack & .mcaddon files into the new Bedrock-Addons folder. 
5. Run the command again to install the packs.
    - Type "bedrock-addons-installer" without the quotes.

#### Command Options
 - bedrock-addons-installer <path_to_server> [-v] [-r]
    - path_to_server - *The relative or full path to the root directory of your server.*
    - -r - *Removes all installed packs before installing the packs from Bedrock-Addons/.*
    - -v - *Enables verbose mode which will log additional details as the script runs.*

#### Notes
 - There are two types of files that this tool can work with. Minecraft packs(.mcpack) which are individual resources, and Minecraft Addons(.mcaddon) which are collections of multiple packs. Minecraft packs will be installed without being altered but the .mcaddon files will be converted into the individual packs it contains before being installed.
    - mySpecialAddon.mcaddon - Converts to ->
        - mySpecialAddon_resource.mcpack
        - mySpecialAddon_behavior.mcpack
 - This tool will check to see if a pack is already installed and up to date. If the new pack has a different version number (even older) it will reinstall the pack. If the versions match nothing will be done.
 - If you want to run a clean installation of all packs you can use the -r option to uninstall all packs before installing those found in the Bedrock-Addons folder. 
 - If you want to completely remove all packs, empty the Bedrock-Addons folder before running the tool with the -r option. 
 - Bedrock Dedicated Servers have required vanilla resources pre-installed. These packs are constantly updated by Mojang, making it difficult to implement a system for differentiating them from custom packs. For this reason the tool assumes that the installed world packs and server packs are synchronized. If you manually installed any pack on just the server, bedrock-addons-installer may have difficulties uninstalling it. 

## Advanced Users (module details)

#### Notes
 - This is a ECMAScript module which makes use of import and export statements.
 - This module uses chegs-simple-logger (https://github.com/chegele/Logger).
 - Install the module locally if you will be using it programmatically. 
    - npm install bedrock-addons-installer --save
 - You will need to manually create a Bedrock-Addons folder at the root of the server.

#### Options
 - **serverPath** *String*   - The path to the root of the Bedrock Dedicated Server.
 - **verboseMode** *Boolean* - [Optional]  Enable all logging details.

#### Functions
 - **installAddon(packPath)** - Installs the individual addon located at the provided path. 
 - **installAllAddons(removeOldPacks)** - Installs all packs in the Bedrock-Addons directory. 
 - **setLogConfig(logConfig)** - Updates logging configuration. https://github.com/chegele/Logger

#### Example
```
import Bedrock Addons Installer from 'bedrock-addons-installer';

let serverPath = '/home/chegele/mcServer/';
let addon = '/home/chegele/mcServer/Bedrock-Addons/CustomAddonTest.mcaddon';

let installer = new BedrockAddonInstaller(serverPath);

// These functions are asynchronous, they will run at the same time.
// You can use then or async/await statements to wit for completion.
installer.installAddon(addon);
installer.installAllAddons();
```
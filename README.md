# TB Blip Creator

A lightweight FiveM blip creation resource that lets players place custom markers on the map and optionally create admin-wide points of interest.

## Features
- Create personal blips with a custom name, sprite, and color
- Create admin blips visible to every player
- Delete your own blips or admin blips if you have access
- Easy-to-use NUI menu
- Persistent storage through the configured database

## Resource Folder Name
Place the folder in your server resources as:

```text
tb_blipcreator
```

Do not rename the folder unless you also update the resource references.

## Requirements
This resource expects a FiveM server with:
- `mysql-async` or another compatible MySQL wrapper
- a working database connection
- a valid server configuration that ensures the resource starts

## Installation
1. Put the resource into your server’s `resources` folder.
2. Make sure the folder name is exactly `tb_blipcreator`.
3. Add it to your server config:

```lua
ensure tb_blipcreator
```

4. Confirm your database is reachable.
5. Configure the resource in [Shared.lua](Shared.lua).

## Database Table
The resource reads and writes from a table named `tb_blips`.

Example schema:

```sql
CREATE TABLE IF NOT EXISTS `tb_blips` (
  `blipid` INT NOT NULL AUTO_INCREMENT,
  `identifier` VARCHAR(255) NOT NULL,
  `x` FLOAT NOT NULL,
  `y` FLOAT NOT NULL,
  `z` FLOAT NOT NULL,
  `sprite` INT NOT NULL,
  `color` INT NOT NULL,
  `name` VARCHAR(255) NOT NULL,
  `universal` TINYINT(1) NOT NULL DEFAULT 0,
  PRIMARY KEY (`blipid`)
);
```

## Configuration
Open [Shared.lua](Shared.lua) and set:
- `Config.Db` to your database type (`mysql`, `ghmattisql`, or `oxmysql`)
- `Config.Identifier` to your preferred identifier type (`license`, `steam`, or `discord`)
- `Config.Admins` with the admin identifiers allowed to create universal blips

Example:

```lua
Config.Db = 'mysql'
Config.Identifier = 'license'
Config.Admins = {
    'license:YOUR_LICENSE_HERE'
}
```

## Command
Use this command in-game:

```text
/blipcreator
```

This opens the NUI blip creator menu.

## How to Use It
1. Open the menu with `/blipcreator`.
2. Enter a blip name.
3. Choose a sprite and color.
4. Press “Get Coords” to capture your current location.
5. Click “Create Blip”.
6. If you are in the admin list, toggle admin mode to create a blip visible to all players.

## Buyer / Seller Notes
- This resource is intended for server owners who want a custom blip-creation system.
- Blips are stored in the database so they persist across restarts.
- Universal blips are meant for shared map markers, server events, or community points of interest.

## Support
This readme is designed to help a buyer or server owner understand the setup and usage quickly. If you are selling or distributing the resource, keep the folder name and config structure intact for compatibility.

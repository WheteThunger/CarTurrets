## Features

- Allow players to deploy auto turrets onto modular cars, at most one per module.
- Limit max turrets per car, optionally using the permissions of the car owner.
- Restrict which modules players can deploy turrets to, using permissions.
- Automatically add turrets to cars when they spawn.
  - Configurable chance to spawn a turret for each module type.
  - Can apply to natural car spawns along the road, as well as other car spawns, optionally requiring the car owner to have permission.
- Configurable turret position for each module type.

#### Notes

- Turrets deployed to the front of the car automatically face forwards, while turrets deployed to the back automatically face backwards. If the default rotation isn't desirable, you can rotate the auto turret like normal once it's deployed.
- Moving a module item between slots will automatically move the turret without rotating it.
- Moving a module item from a car's inventory to your inventory, or dropping it from the car's inventory, will automatically add an auto turret item to your inventory (if the module had a turret) with condition matching the auto turret's health, unless the `EnableTurretPickup` configuration option is `false`.
- Turrets deployed to vehicle modules will not target NPC players or non-hostile players who are in safe zones.

## How To Use

There are two ways to deploy an auto turret to a car module.
- Aim at a car module and use the `carturret` command
- While editing a car at a lift, click and drag an auto turret item onto one of the car's modules

Deploying an auto turret to a car module will consume an auto turret item from the player's inventory. Deploying turrets can be free for players with additional permissions, but an auto turret will still be required in their inventory in order to use the drag-and-drop method.

## Commands

- `carturret` -- Deploy an auto turret onto the car module you are aiming at. You must not be building blocked. You must be within several meters of the car.

## Permissions

- `carturrets.deploy.command` -- Allows the player to use the `carturret` command. Note: The player also requires module-specific permissions for that command to work.
- `carturrets.deploy.inventory` -- Allows the player to deploy an auto turret to a vehicle module by clicking and dragging an auto turret item onto a vehicle module item in a car's inventory while editing the car at a lift. Note: The player also requires module-specific permissions for this to work.
- `carturrets.spawnwithcar` -- Cars owned by players with this permission will spawn with turrets automatically added to each module they have permission to, up to the limit they are allowed. The chance for each module to spawn with a turret is determined by the plugin configuration under `SpawnWithCar->SpawnChanceByModule`.
  - Only applicable if the plugin configuration for `SpawnWithCar->OtherCarSpawns->Enabled` is `true`, and only necessary if `SpawnWithCar->OtherCarSpawns->RequirePermission` is `true`.
- `carturrets.allmodules` -- Allows the player to deploy turrets to all module types.

As an alternative to the `allmodules` permission, you can grant permissions by module type (these are generated from the config):
- `carturrets.vehicle.1mod.cockpit`
- `carturrets.vehicle.1mod.cockpit.armored`
- `carturrets.vehicle.1mod.cockpit.with.engine`
- `carturrets.vehicle.1mod.engine`
- `carturrets.vehicle.1mod.flatbed`
- `carturrets.vehicle.1mod.passengers.armored`
- `carturrets.vehicle.1mod.rear.seats`
- `carturrets.vehicle.1mod.storage`
- `carturrets.vehicle.1mod.taxi`
- `carturrets.vehicle.2mod.flatbed`
- `carturrets.vehicle.2mod.fuel.tank`
- `carturrets.vehicle.2mod.passengers`

The following permissions determine the maximum number of turrets that can be deployed to a car owned by the player, overriding the `DefaultLimitPerCar` option in the plugin configuration.
- `carturrets.limit.2` -- Allows cars owned by the player to receive at most 2 turrets.
- `carturrets.limit.3` -- Allows cars owned by the player to receive at most 3 turrets.
- `carturrets.limit.4` -- Allows cars owned by the player to receive at most 4 turrets.

If multiple of these permissions are granted to a player, the highest will be used.

Car ownership is determined by the `OwnerID` property of the car, which is usually a player's Steam ID, or `0` for no owner. Various plugins can spawn cars with a set owner, such as [Spawn Modular Car](https://umod.org/plugins/spawn-modular-car) or [Craft Car Chassis](https://umod.org/plugins/craft-car-chassis), while other plugins allow the owner to change with certain events, such as [Claim Vehicle Ownership](https://umod.org/plugins/claim-vehicle-ownership).

## Configuration

```json
{
  "DefaultLimitPerCar": 4,
  "EnableTurretPickup": true,
  "SpawnWithCar": {
    "NaturalCarSpawns": {
      "Enabled": false
    },
    "OtherCarSpawns": {
      "Enabled": false,
      "RequirePermission": false
    },
    "SpawnChanceByModule": {
      "vehicle.1mod.cockpit": 0,
      "vehicle.1mod.cockpit.armored": 0,
      "vehicle.1mod.cockpit.with.engine": 0,
      "vehicle.1mod.engine": 0,
      "vehicle.1mod.flatbed": 0,
      "vehicle.1mod.passengers.armored": 0,
      "vehicle.1mod.rear.seats": 0,
      "vehicle.1mod.storage": 0,
      "vehicle.1mod.taxi": 0,
      "vehicle.2mod.flatbed": 0,
      "vehicle.2mod.fuel.tank": 0,
      "vehicle.2mod.passengers": 0
    }
  },
  "AutoTurretPositionByModule": {
    "vehicle.1mod.cockpit": {
      "x": 0.0,
      "y": 1.39,
      "z": -0.3
    },
    "vehicle.1mod.cockpit.armored": {
      "x": 0.0,
      "y": 1.39,
      "z": -0.3
    },
    "vehicle.1mod.cockpit.with.engine": {
      "x": 0.0,
      "y": 1.39,
      "z": -0.85
    },
    "vehicle.1mod.engine": {
      "x": 0.0,
      "y": 0.4,
      "z": 0.0
    },
    "vehicle.1mod.flatbed": {
      "x": 0.0,
      "y": 0.06,
      "z": 0.0
    },
    "vehicle.1mod.passengers.armored": {
      "x": 0.0,
      "y": 1.38,
      "z": -0.31
    },
    "vehicle.1mod.rear.seats": {
      "x": 0.0,
      "y": 1.4,
      "z": -0.12
    },
    "vehicle.1mod.storage": {
      "x": 0.0,
      "y": 0.61,
      "z": 0.0
    },
    "vehicle.1mod.taxi": {
      "x": 0.0,
      "y": 1.38,
      "z": -0.13
    },
    "vehicle.2mod.flatbed": {
      "x": 0.0,
      "y": 0.06,
      "z": -0.7
    },
    "vehicle.2mod.fuel.tank": {
      "x": 0.0,
      "y": 1.28,
      "z": -0.85
    },
    "vehicle.2mod.passengers": {
      "x": 0.0,
      "y": 1.4,
      "z": -0.9
    }
  }
}
```

- `DefaultLimitPerCar` -- The maximum number of auto turrets allowed per car. Cars owned by players with additional permissions may have a higher value. Regardless of this value, the number of auto turrets cannot exceed the number of modules on the car.
  - Note: You can also reduce the practical limit of auto turrets per car by restricting which modules they can be deployed to. For example, if you only allow auto turrets to be deployed to flatbed modules, a 2-socket car can have at most one auto turret (assuming it's driveable). For longer cars, players will have to choose between more turrets and other utilities. You can also restrict turrets to only 2-socket modules.
- `EnableTurretPickup` (`true` or `false`) -- While `false`, car turrets cannot be picked up with a hammer or with the RemoverTool pugin, and removing a module from a car will destroy the turret without adding an auto turret item to the player inventory.
- `SpawnWithCar` -- Settings for automatically adding turrets to cars when they spawn.
  - `NaturalCarSpawns`
    - `Enabled` (`true` or `false`) -- While `true`, cars that spawn naturally along roads will automatically have turrets added to them, up to the limit determined by `DefaultLimitPerCar`, and according to the chances in `SpawnChanceByModule`.
  - `OtherCarSpawns`.
    - `Enabled` (`true` or `false`) -- While `true`, cars spawned by plugins (such as [Spawn Modular Car](https://umod.org/plugins/spawn-modular-car) or Vehicle Airdrops) will have turrets added to them automatically, up to the limit determined by `DefaultLimitPerCar` or based on the permissions of the car owner if applicable, and according to the chances in `SpawnChanceByModule`.
    - `RequirePermission` (`true` or `false`) -- While `true`, cars spawned by plugins will only have turrets added to them if the car is owned by a player with the `carturrets.spawnwithcar` permission.
  - `SpawnChanceByModule` -- For each module type (based on item short name), these values determine the percent chance (`0` - `100`) that modules of that type will automatically have a turret added to them when the car spawns.
- `AutoTurretPositionByModule` -- For each module type (based on item short name), these values determine how an auto turret will be positioned relative to its parent module. These defaults were tested with modules in various positions with turrets facing forwards and backwards. Some modules, especially the small engine cockpit module, simply don't have an ideal position due to having a very small roof, but careful placement of modules and turrets can avoid any visual issues.

## Localization

```json
{
  "Generic.Error.NoPermission": "You don't have permission to do that.",
  "Generic.Error.BuildingBlocked": "Error: Cannot do that while building blocked.",
  "Deploy.Error.NoCarFound": "Error: No car found.",
  "Deploy.Error.NoModules": "Error: That car has no modules.",
  "Deploy.Error.NoPermissionToModule": "You don't have permission to do that to that module type.",
  "Deploy.Error.ModuleAlreadyHasTurret": "Error: That module already has a turret.",
  "Deploy.Error.UnsupportedModule": "Error: That module is not supported.",
  "Deploy.Error.TurretLimit": "Error: That car may only have {0} turret(s).",
  "Deploy.Error.NoSuitableModule": "Error: No suitable module found.",
  "Deploy.Error.NoTurret": "Error: You need an auto turret to do that.",
  "Remove.Error.TurretHasItems": "Error: That module's turret must be empty."
}
```

## Plugin Compatibility

- Compatible with plugins such as [Turret Loadouts](https://umod.org/plugins/turret-loadouts) and [Turret Manager](https://umod.org/plugins/turret-manager) that automatically fill turrets with weapons and ammo when deployed.
- Compatible with [Vehicle Deployed Locks](https://umod.org/plugins/vehicle-deployed-locks). Players who do not have access to the lock cannot flip the switch or authorize themselves to the turret.
- **Recommended:** [Better Turret Aim](https://umod.org/plugins/better-turret-aim) allows turrets to aim at their current target more quickly. Very useful for vehicle turrets to be able to hit targets while the vehicle is moving. Has an option to only apply to vehicle turrets if desired.

## Developer API

#### API_DeployAutoTurret

Plugins can call this API to deploy an auto turret to a car module. The `BasePlayer` parameter is optional, but providing it is recommended as it will automatically authorize the player and allows for compatibility with plugins that automatically add weapons and ammo to the turret when deployed.

Note: This bypasses several checks, such as permissions, whether the player is building blocked, and the car's turret limit.

```csharp
AutoTurret API_DeployAutoTurret(BaseVehicleModule module, BasePlayer player)
```

The return value will be the newly deployed auto turret, or `null` if the auto turret was not deployed for any of the following reasons.
- The module type is unsupported (i.e., not defined in the config)
- The specified module already has a turret on it

## Developer Hooks

#### OnCarAutoTurretDeploy

- Called when a player or a plugin tries to deploy an auto turret to a car module.
- Returning `false` will prevent the auto turret from being deployed. None of the player's items will be consumed.
- Returning `null` will result in the default behavior.

Note: The `BasePlayer` parameter may be null if another plugin initiated the deployment without specifying a player.

```csharp
object OnCarAutoTurretDeploy(BaseVehicleModule module, BasePlayer player, bool automatedDeployment)
```

If your plugin is using this hook to block turrets from being deployed to a particular car, it's recommended that you print a relevant message to the user's chat to inform them of why it was blocked.

If the `automatedDeployment` argument is `true`, that indicates this plugin attempted to deploy the turret automatically as the car was spawning. In that case, the hook will be called for each turret that this plugin attempts to add (up to 4 times), so you should refrain from messaging the user in that case to avoid spamming them.

#### OnEntityBuilt

This is an Oxide hook that is normally called when deploying an auto turret or other deployable. To allow for compatibility with other plugins, this plugin calls this hook whenever an auto turret is deployed to a car module for a player.

Note: This is not called when an auto turret is deployed via the API without specifying a player.

```csharp
void OnEntityBuilt(Planner planner, GameObject go)
```

The `Planner` can be used to get the player or the auto turret item, while the `GameObject` can be used to get the deployed auto turret.

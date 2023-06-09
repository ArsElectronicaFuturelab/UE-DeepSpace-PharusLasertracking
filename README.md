# UE-DeepSpace-Pharus Lasertracking
## Table of Contents
1. [Quick links](#quick-links)
2. [Overview](#overview)
3. [Folder Structure](#folder-structure)
5. [Prerequisites](#prerequisites)
4. [Configuration](#configuration)
6. [Quickstart Project](#quickstart-project)
7. [Quickstart Project and Plugin with Switchboard](#quickstart-project-and-plugin-with-switchboard)
8. [Development](#development)
9. [Production](#production)

## Quick links
Download UE DeepSpace Starter (Zips)
* [UE 4.27 DeepSpace Starter](https://github.com/ArsElectronicaFuturelab/UE-DeepSpace-Starter/archive/refs/heads/UE-4.27.2-DeepSpace-Starter.zip)
* [UE 5.0 DeepSpace Starter](https://github.com/ArsElectronicaFuturelab/UE-DeepSpace-Starter/archive/refs/heads/UE-5.0-DeepSpace-Starter.zip)
* [UE 5.1 DeepSpace Starter](https://github.com/ArsElectronicaFuturelab/UE-DeepSpace-Starter/archive/refs/heads/UE-5.1-DeepSpace-Starter.zip)

Download UE Pharus DeepSpace Plugin
* [UE 4.27 Pharus Lasertracking](https://github.com/ArsElectronicaFuturelab/UE-DeepSpace-PharusLasertracking/archive/refs/heads/UE-4.27-Pharus-Lasertracking-Plugin.zip)
* [UE 5.0 Pharus Lasertracking](https://github.com/ArsElectronicaFuturelab/UE-DeepSpace-PharusLasertracking/archive/refs/heads/UE-5.0-Pharus-Lasertracking-Plugin.zip)
* [UE 5.1 Pharus Lasertracking](https://github.com/ArsElectronicaFuturelab/UE-DeepSpace-PharusLasertracking/archive/refs/heads/UE-5.1-Pharus-Lasertracking-Plugin.zip)

## Overview
The Pharus tracking system, developed by researcher and artist [Otto Naderer](https://ars.electronica.art/futurelab/en/naderer-otto/) at [Ars Electronica Futurelab](https://ars.electronica.art/futurelab/en) enables interaction opportunities for groups of any size in various environments. Learn more [...](https://ars.electronica.art/futurelab/en/projects-phar)

The Plugin serves as an extension for [UE-DeepSpace Starter](https://github.com/ArsElectronicaFuturelab/UE-DeepSpace-Starter). Additionally, the project includes simulation software to aid in the development process.

![Example 1](https://github.com/ArsElectronicaFuturelab/UE-DeepSpace-PharusLasertracking/blob/main/Files/pharus-example-view-in-editor-1.png)
![Example 2](https://github.com/ArsElectronicaFuturelab/UE-DeepSpace-PharusLasertracking/blob/main/Files/pharus-example-view-in-editor-2.png)
![Example 3](https://github.com/ArsElectronicaFuturelab/UE-DeepSpace-PharusLasertracking/blob/main/Files/pharus-example-view-in-editor-3.png)

## Folder Structure
    \PharusSimulators           -> Simulators for testing
    \Plugins                    -> Contains a file manager and the pharus plugin

## Prerequisites 
* Download/Install DBJson Plugin from the Unreal Engine Market-Place [DBJson](https://www.unrealengine.com/marketplace/en-US/product/dbjson). This plugin is required to load a custom json file, which is located in /Content/DeepSpace/Settings/pharus-config.json
* Download [DeepSpace Starter](https://github.com/ArsElectronicaFuturelab/UE-DeepSpace-Starter) template to integrate this plugin

## Configuration
* Customize the Pharus config file "\DeepSpaceStarter\Content\DeepSpace\Settings\pharus-config.json" according to your needs.

## Quickstart Project
* Run "PharusSimulators/PharusRecSimulator/bin/start_limelight1.bat"
* Enable "Show Plugin Content" in Unreal Engine Content Browser Settings
* Load Map "/Plugins/PharusLasertracking/Content/Pharus/Maps/Pharus_SpawnAndUpdate_Map.umap"
* Hit Play in the Editor

## Quickstart Project and Plugin with Switchboard
Follow these steps [Quickstart Project with Switchboard](https://github.com/ArsElectronicaFuturelab/UE-DeepSpace-Starter#quickstart-project-with-switchboard):
* Switchboard
   * Choose the "Pharus_StartMap" in the "Level" select option
   * Add Device/nDisplay Cluster
      * Click "Populate"
      * Choose "nDisplay_Desktop.uasset" or "nDisplay_Desktop_2_Views.uasset"
   * Click the Plugin-Icon in the table header (connects to listener)

## Development
In the "Plugins/PharusLasertracking/core", you'll find the "BP_PharusTracker_Manager". This Blueprint needs to be dropped into the world. If you have a custom map, please refer to "Pharus_StartMap" to see how and where the tracking manager is placed. The default settings should work out of the box.

When changes are made to the Pharus-Tracker-Manager, enter the following values to reset to the default.
* DebugPublicInt: 0
* PharusTrackerIsMultiCast: [x]
* PharusTrackerUDPPort: 44345
* PharusTrackerBindNIC: 127.0.0.1
* XSize: 80.0
* YSize: 100.0
This settings are only used as fallback, when the pharus config file "\DeepSpaceStarter\Content\DeepSpace\Settings\pharus-config.json" is not found.

To spawn objects, it is necessary to set the spawn class in the Pharus tracker panel group in the details. A spawned actor must implement the "PharusActorInterface". The interface is responsible to set the actor track id to a spawned actor You find some example spawn actors in "/Plugins/PharusLasertracking/SpawnExampleActors"

## Production
To make use of your project with the Pharus plugin in the Ars Electronica DeepSpace, you should update the configuration file located at "\DeepSpaceStarter\Content\DeepSpace\Settings\pharus-config.json". Configure the pharusTrackerBindNIC to be either 192.168.19.114 (Wall) or 192.168.19.115 (Floor) before packaging the project.

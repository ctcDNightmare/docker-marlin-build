## Build Marlin firmware using docker

This is a simple repository for using docker to build Marlin firmware for 3d-printers.

The `./build-marlin.sh` script does the following

1. Builds the docker image, or skips build if you already created one on the current date.
2. Prompts if you wish to fetch the latest MarlinFirmware release, with option to disable prompt using a `UPDATE_SKIP=yes` local variable set in your shell.
3. Changes the `default_envs` variable in `platformio.ini` to the value defined in the `board` file inside CustomConfiguration.
4. Then it copies all `.h` files from the CustomConfiguration folder, into the `MarlinFirmware/Marlin` folder, replacing the destination files.
5. Uses a docker container to build firmware, using `platformio core` on a non-root user.
6. Output the compiled firmware location.

### Custom Configuration

The included configuration is for my `Ender-3 Pro` running with a `SKR Mini E3 V1.2`.

You can fork this repository to adapt the configuration for your printer, you can always update the fork if there are any updates on this repository.

Other Marlin configuration examples can be [found here.](https://github.com/MarlinFirmware/Configurations/tree/import-2.0.x/config/examples)


### Advanced Configuration

In some cases you might have the need to change variables not covered by `.h` configuration files, and require to make changes inside the `MarlinFirmware/Marlin/src` folder.

The script currently have no logic for replacing files inside sub-folders, so i recommend you to update the `MarlinFirmware` submodule once, and then set the `UPDATE_SKIP=yes` local variable, so that you can edit the files inside `MarlinFirmware/Marlin/src` folder without the changes being discarded due to git hard reset.

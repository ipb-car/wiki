[//]: <> (0. Did you... turn on your brain??)

1. Did you turn on the power (battery and hub) and connected all the cables _correctly_? Check thunderbolt connection to polenta and setup too!
1. The Raspberry Pi ptpd sync takes awhile to start, so maybe wait for a few seconds.
1. Did you check if the code base is up to date with remote? (maybe try `git submodule update`)
1. Did you make sure the GPS antenna is outside (to receive GPS signal)?
1. Did you check the network connection on polenta? (it should be set to the connection of the thunderbolt interface)
1. If you have issues where the ros package cannot be found, maybe check the necessary scripts have been sourced.

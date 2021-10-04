# Configuration files/Command line

JARs can be configured through files.

Located in src/main/resources, editables files are:
  
* globals/game_preferences.json: timeouts of lobby, turns, etc.
* globals/connection_globals.json: ip, ports, adresses
* boards/boards.json: edit and add new boards
* logs/logger_std_config.json:  modify logger settings, like filterLevel (0 to 5), or enabling colors in the terminal

Client's command line arguments:

* `-i`: visualize help
* `-u <cli/gui>` select client's interface
* `-c <rmi/socket>` select client's connection
* `-i <indirizzo ip>` sepcify server's IP adress
* `-n <nickname>` specify client's nickname

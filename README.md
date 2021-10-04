# Sagrada - Boardgame

This repo contains the final project for the Computer Science and Engineering
Bachelor Degree course [*PROVA FINALE (INGEGNERIA DEL SOFTWARE)*
(085923 - A.Y. 2017/18)][course] of Politecnico di Milano. The goal of the
project is to implement the boardgame [Sagrada][sagrada].

* Authors: [Leonardo Barilani][author-1], [William Bonvini][author-2], [Lorenzo Carnaghi][author-3]
* Assignement: [ITA](doc/Requisiti.pdf), [ENG summary](doc/Requirements.md)
* [Configuration](doc/Configuration.md)

## Main Features

* Complete rules of the game
* RMI Networking
* Socket Networking
* Management of network failure: disconnection & reconnection
* Graphical user interface (GUI)
* Command line interface (CLI)
* Handling multiple matches at the same time on the same server
* Complete configuration of maps via JSON files
* Complete configuration of parameters via JSON files
* Complete configuration of game rules via JSON files

## Design Choices and Implementation

* [High Level UML](doc/HighLevelUML.pdf)
* [Low Level UML](doc/LowLevelUML.pdf)
* [Connection protocol](doc/ConnectionProtocol.md)
* [Modular Game Rules Implementation](doc/ModularGameRulesImplementation.md)

## Screenshots

### GUI interface

<img src="./screenshots/GUI.png" width="400" height="auto">

### CLI interface

<img src="./screenshots/CLI.png" width="400" height="auto">

## Copyrighted images

Given the academic nature of the project and to avoid legal issues, the images provided are not from the original game. Instead, they have been replaced with blank placeholders, so that the project compiles without encountering missing files errors.

---

[course]: https://www4.ceda.polimi.it/manifesti/manifesti/controller/ManifestoPublic.do?EVN_DETTAGLIO_RIGA_MANIFESTO=evento&aa=2017&k_cf=225&k_corso_la=358&k_indir=II3&codDescr=085923&lang=IT&semestre=2&anno_corso=3&idItemOfferta=133689&idRiga=221825
[sagrada]: https://boardgamegeek.com/boardgame/199561/sagrada
[author-1]: https://github.com/leonardobarilani
[author-2]: https://github.com/WilliamBonvini
[author-3]: https://github.com/Lockyard

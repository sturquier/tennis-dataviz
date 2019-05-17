# Tennis data challenge

## Data dictionnary

|           Variable           |           English Version          |                                                Description                                                |                        Valeur                       |
|:----------------------------:|:----------------------------------:|:---------------------------------------------------------------------------------------------------------:|:---------------------------------------------------:|
| échange                      | rally                              | le nombre de coups échangés pour le point                                                                 | integer from 1, 2, 3.. pas de 1 (no ace)            |
| service                      | serve                              | un indicateur qui permet de savoir si le point a été joué sur le 1er ou 2nd service                       | 1 = First, 2 = Second                                |
| type                         | hitpoint                           | manière dont le dernier coup est joué                                                                     | F = coup droit, B = revers, V = volée, U = inconnu     |
| vitesse                      | speed                              | vitesse du dernier coup                                                                                   | Continous (m/s)                                     |
| dégagement filet             | net.clearance                      | distance au dessus du filet entre le filet et la balle pour le dernier coup                               | continous (cm) valeur possiblement négative         |
| distance ligne de touche     | distance.from.sideline             | Distance latérale entre le rebond du dernier coup et la ligne de touche                                   | mètres >= 0                                         |
| profondeur                   | depth                              | Distance entre le rebond du dernier coup et le fond de cour                                               | mètres >= 0                                         |
| en dehors de la ligne        | outside.sideline                   | Indicateur logique si le dernier coup était en dehors de la ligne de touche                               | bool                                                |
| au dela du fond de cour      | outside.baseline                   | Indicateur logique si le dernier coup était au dela du fond de cour                                       | bool                                                |
| distance joueur              | player.distance.travelled          | Distance du joueur qui a gagné le point entre l'impact de l'avant dernier tir et l'impact du dernier tir. | mètres                                              |
| distance joueur 2            | player.impact.depth                | Distance entre le joueur gagnant et le filet au moment ou le dernier coup a été tiré.                     | mètres                                              |
| distance joueur 3            | player.impact.distance.from.center | Distance entre le joueur gagnant et la ligne centrale au moment ou le dernier coup a été tiré.            | mètres                                              |
| distance joueur 4            | player.depth                       | Distance entre le joueur gagnant et le filet au moment ou l'avant dernier coup a été tiré.                | mètres                                              |
| distance joueur 5            | player.distance.from.center        | Distance entre le joueur gagnant et la ligne centrale au moment ou l'avant dernier coup a été tiré        | mètres                                              |
| distance adversaire          | opponent.depth                     | Distance entre l'adversaire et le filet au moment ou l'avant dernier coup a été tiré                      | mètres                                              |
| distance adversaire 2        | opponent.distance.from.center      | Distance entre l'adversaire et la ligne centrale au moment ou l'avant dernier coup a été tiré             | mètres                                              |
|                              | same.side                          | Savoir si les deux joueurs ?                                                                              | bool                                                |
| vitesse avant dernier tir    | previous.speed                     | Vitesse de l'avant dernier tir                                                                            | continous (m/s)                                     |
| distance avd filet           | previous.net.clearance             | Distance au dessus du filet, entre le filet et l'avant dernier tir                                        | continous (cm) possible négatif                     |
| distance rebond ligne touche | previous.distance.from.sideline    | Distance entre l'avant dernier rebond et la plus proche ligne de touche                                   | mètres >= 0                                         |
| précedente profondeur        | previous.depth                     | Distance entre le rebond de l'avant dernier coup et le fond de cour                                       | mètres >= 0                                         |
| précédente catégorie         | previous.hitpoint                  | Categorie de l'avant dernier tir                                                                          | F = coup droit, B = revers, V = volée, U = inconnu     |
| tps avant dernier tir filet  | previous.time.to.net               | Temps que l'avant dernier tir a pris pour passer le filet                                                 | continous number (sec)                              |
| impact service joueur        | server.is.impact.player            | Si le joueur qui a marqué le point était celui qui a servi                                                | bool                                                |
| Catégorie tir                | outcome                            | Catégorie du tir gagnant                                                                                  | W : gagnant, FE : Erreur forcé, UE : Erreur non forcé |
| id                           | id                                 | id unique de 10 caractères                                                                                | char                                                |

Trucs chelous ( `describe()` ) :
* Homme
	* net.clearance : 12 max
	* distance.from.sideline : 16 max
	* opponent.depth : 20 max
	* opponent.distance.from.center : 13 max
* Femme
	* net.clearance : 6 max
	* distance.from.sideline (?) : 12 max
	* opponent.depth (?) : 17 max

Data représentable :
* Basic
	* Rally
	* Serve
	* hitpoint (countplot)
	* outcome (countplot)
	*

Data aggrégable :
* **hitpoint / outcome** ( est ce que la manière dont le dernier coup a été joué ( coup droit / revers ) est corrélé avec la catég gagnante ?
* **speed / previous.speed** ( est ce que la difference de vitesse est impactante ? )
* **same.side / hitpoint** ( est ce que le fait que les joueurs soient du même coté va impacter la facon dont le coup est joué ? + voir données cohérentes )
* Où le joueur gagnant est-il situé sur le terrain ? Son positionnement a-t-il un impact sur la victoire ?
	* **player.impact.depth** ( gagnant est-il loin/près du filet au tir du dernier coup ? )
	* **player.impact.distance.from.center** ( gagnant est-il loin/près de la ligne centrale au tir du dernier coup ? )
* Où le joueur perdant est-il situé sur le terrain ? Son positionnement a-t-il un impact sur la défaite ?
	* **opponent.depth** ( perdant est-il loin/près du filet au tir de l'avant dernier coup ? )
	* **opponent.distance.from.center** ( perdant est-il loin/près de la ligne centrale au tir de l'avant dernier coup ? )
* Lorsque faute ( direct / indirect ) , où était la balle lors du dernier coup ( en dehors de la ligne de touche / au dela du fond de cours ? )
	* **outside.sideline / outcome** 
	* **outside.baseline / outcome**
* Corrélation entre vitesse du dernier coup gagnant & sa catégorie **speed/outcome**

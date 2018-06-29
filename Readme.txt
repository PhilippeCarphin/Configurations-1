Le bout qui utilise la fonction readlink et tout est expliqué dans le post sur
stackOverflow mais voici pourquoi il est là.

C'est pour déterminer où le script et tes fichiers sont. Par exemple, si tes
fichires sont dans

	~/.victorconfig

et que l'emplacement de ce script est

	~/.victorconfig/install.sh

mais que pour une raison ou une autre, tu as un lien

	~/.install.sh -> ~/.victorconfig/install.sh

, alors dans le script, si tu exécute

	[ ~ ] $ ./install.sh

alors $0 dans ce cas sera ~/.install.sh et on ne saura pas vraiment ou sont
tes fichiers.

C'est une situation commune d'avoir un lien vers un script et que ce script
veuille savoir où il est.  Mais puisqu'on l'appelle à travers un lien, il ne
peut pas utiliser la variable $0 pour savoir où il est.

Pour cette raison, on utilise le bout de code suivant pour aller chercher
l'endroit vers lequel le lien pointe.  Il faut noter que ceci va seulement
marcher pour un lien.  Mais de toutes façons c'est en masse puisqu'il n'y a
presqu'aucune raison de faire un lien vers un tel script.


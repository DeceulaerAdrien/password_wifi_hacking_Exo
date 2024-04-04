# Password Wifi Hacking

# Rapport d'exercice sur le piratage du réseau WiFi du routeur de test

## Objectif

Ce rapport résume les étapes suivies pour pirater le réseau WiFi du routeur de test, en utilisant les outils disponibles dans la suite logicielle Kali Linux et en se basant sur l'apprentissage rapide du module TryHackMe [Wifi Hacking 101](https://www.notion.so/Wifi-Hacking-101-9b3042ce9edf461cb4103cdc349af7fd?pvs=21).

## Étapes suivies

1. **Apprentissage rapide du module TryHackMe [Wifi Hacking 101](https://www.notion.so/Wifi-Hacking-101-9b3042ce9edf461cb4103cdc349af7fd?pvs=21).**
2. Utilisation de la commande `iwconfig` pour voir les interfaces réseau connectées.
3. Utilisation des outils air...-ng intégrés de base dans Kali Linux.
4. Passage de mon interface en mode monitoring grâce à l'outil `airmon-ng` et la commande suivante :
    
    ```bash
    airmon-ng start <nom_de_l_interface>
    
    ```
    
5. Utilisation de l'interface en mode monitoring pour analyser tous les réseaux WiFi détectables avec l'outil `airodump-ng` et la commande suivante :
    
    ```bash
    airodump-ng <nom_de_l_interface_sous_monitoring>
    
    ```
    
    ![Password%20Wifi%20Hacking%20b165b2f44d1f4d9c9172ef9620409d4d/fa098146-c6ee-4d57-bf63-3882b7b0eda9.png](Password%20Wifi%20Hacking%20b165b2f44d1f4d9c9172ef9620409d4d/fa098146-c6ee-4d57-bf63-3882b7b0eda9.png)
    
6. Utilisation de l'outil `airodump-ng` sur le réseau sélectionné pour surveiller le trafic sur le canal de la connexion et enregistrer dans un fichier :
    
    ```bash
    airodump-ng -c <canal> -d <BSSID> <INTERFACE_MONITORING> -w <nom_du_fichier>
    
    ```
    
    ![Password%20Wifi%20Hacking%20b165b2f44d1f4d9c9172ef9620409d4d/2869d477-6acd-4c05-be2b-e2ab3072aadc.png](Password%20Wifi%20Hacking%20b165b2f44d1f4d9c9172ef9620409d4d/2869d477-6acd-4c05-be2b-e2ab3072aadc.png)
    
7. Utilisation de l'outil `airplay-ng` pour envoyer des paquets de données au routeur ciblé et intercepter les paquets d'authentification :
    
    ```bash
    airplay-ng --deauth -a <BSSID_CIBLE> -c <BSSID_DESTINATION(le_votre)> <INTERFACE_MONITORING>
    
    ```
    
8. Arrêt de l'envoi après quelques minutes en utilisant CTRL+C et utilisation de Wireshark sur le fichier `.cap` (par défaut dans votre dossier utilisateur) pour rechercher les paquets avec le protocole EAPOL. Si ces paquets sont présents, passer à l'étape suivante ; sinon, refaire une injection de paquets avec `airplay-ng` pendant une durée plus longue.
9. Utilisation de l'outil `aircrack-ng` avec le fichier `.cap` et un dictionnaire de mots (par exemple, rockyou). La comparaison des paquets avec la liste de mots permet de trouver le mot de passe :
    
    ```bash
    aircrack-ng <fichier_.cap> -w <liste_de_mots>
    
    ```
    
    ![Password%20Wifi%20Hacking%20b165b2f44d1f4d9c9172ef9620409d4d/009b0fab-0824-4464-914d-2ed707c03a71.png](Password%20Wifi%20Hacking%20b165b2f44d1f4d9c9172ef9620409d4d/009b0fab-0824-4464-914d-2ed707c03a71.png)
    

## Remarque

Ce rapport se concentre sur ma compréhension de l'exercice. Certaines données ou explications peuvent être erronées et sujettes à changement.
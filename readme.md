Voici la correction du texte avec des fautes corrigées :

---

# Bibliothèque utilisée 

Environnement conda -> smb://192.168.10.11/Commun/Services/IA/Env/obione_1.yaml   Date : 18/10/2024

# Objectifs : 
- Éviter d'annoter des images qui apportent peu de nouvelles informations
    - Permet d'annoter moins d'images 
    - Permet d'obtenir un ensemble d'entraînement plus diversifié et compact, et donc un entraînement plus rapide 

# Fonctionnement :
1. On utilise ResNet50 pour extraire les caractéristiques/features des images (mesure de leur similarité).
2. On utilise K-means pour créer un nombre x de clusters d'images similaires.
3. On sélectionne un pourcentage non linéaire dans chaque cluster :
    - Plus le cluster contient d'images, moins on en prend.
    - Moins le cluster contient d'images, plus on en prend.

Plus il y a de clusters, plus on capture des images présentant des différences subtiles.

# Fichiers CSV créés : 
**feature.csv** -> Contient les caractéristiques de chaque image présente dans le dossier.
**clustered_features_all.csv** -> Récupère tous les features.csv et crée des clusters définis par K-means.

# Options :
- INFO_DEBUG -> Affiche des messages pour suivre l'avancement du code.
- FOLDER_DATA_EXPORT  -> Dossier où exporter le set d'entraînement.
- FOLDER_DATA_IMPORT  -> Dossier où importer les images.
- FOLDER_IMAGE = [] -> Liste des images à utiliser.

- GET_FEATURE = True  -> Crée un fichier feature.csv dans le dossier des images importées.
- REPLACE_FEATURE_IF_EXIST -> Passe au dossier suivant si le fichier feature existe déjà.

- GET_CLUSTER  -> Si False, ne crée pas le fichier clustered_features_all.csv.
- EXPORT  -> Si True, exporte les images sélectionnées par cluster.

# Options pour le nombre de clusters 
- NB_CLUSTER = 20  # Nombre de groupes créés en fonction des caractéristiques.

# Paramètres de sélection par cluster 
- P_MIN   -> Pourcentage minimal si le cluster contient **beaucoup d'images**
- P_MAX   -> Pourcentage maximal si le cluster contient **peu d'images**
- FACTEUR_CROISSANCE  -> Facteur de décroissance exponentielle ; plus il est grand, plus la décroissance des probabilités est rapide.

# Score de similitude : 
Plus le nombre d'expériences est élevé, plus le score de similitude de notre jeu de données reflète la similarité des images.
Plus on se rapproche de 0, plus le jeu de données contient des images sensiblement différentes.
- EXPERIENCE_SCORE_SIMILITUDE = True
- NB_EXPERIENCE_SIMILITUDE = 100
# IMGsimilators

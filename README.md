# 🚀 Guide pour Utiliser WSL avec PyTorch et ROCm

Ce guide explique comment utiliser votre environnement WSL2 (Windows Subsystem for Linux) pour travailler avec PyTorch sur GPU.

##  1. Accéder à WSL
###  Pour démarrer l'environnement WSL :

1. Ouvrir PowerShell ou CMD :

```
wsl -d Ubuntu-22.04
```
- Ca connectera à l'instance WSL nommée Ubuntu-22.04

2. Vérifier votre version de Linux (facultatif) :

```
lsb_release -a
```
##  2. Activer l’environnement virtuel Python

### Étape 1 : Créer ou copier l’environnement virtuel et les fichiers nécessaires

1. Créer un nouvel environnement virtuel (si besoin):

Si vous n’avez pas encore d’environnement virtuel pour le projet, créez-en un dans votre dossier projet :

```
python3.10 -m venv .venv
```

2. Télécharger les fichiers nécessaires à PyTorch avec support GPU ROCm :
Exécutez les commandes suivantes pour télécharger les fichiers .whl requis :

```
wget https://repo.radeon.com/rocm/manylinux/rocm-rel-6.1.3/torch-2.1.2%2Brocm6.1.3-cp310-cp310-linux_x86_64.whl
wget https://repo.radeon.com/rocm/manylinux/rocm-rel-6.1.3/torchvision-0.16.1%2Brocm6.1.3-cp310-cp310-linux_x86_64.whl
wget https://repo.radeon.com/rocm/manylinux/rocm-rel-6.1.3/pytorch_triton_rocm-2.1.0%2Brocm6.1.3.4d510c3a44-cp310-cp310-linux_x86_64.whl
```

3. Copier un .venv existant (optionnel) :

Si vous avez déjà un environnement virtuel configuré pour le GPU dans un autre projet, copiez-le dans votre nouveau projet :

exemple : 

```
cp -r ~/<nom_du_modèle>_model/.venv ./
```

4. Installer PyTorch et ses dépendances :

Si vous avez téléchargé les fichiers ```.whl```, installez-les dans votre environnement virtuel :

```
pip install torch-2.1.2+rocm6.1.3-cp310-cp310-linux_x86_64.whl \
            torchvision-0.16.1+rocm6.1.3-cp310-cp310-linux_x86_64.whl \
            pytorch_triton_rocm-2.1.0+rocm6.1.3.4d510c3a44-cp310-cp310-linux_x86_64.whl
```


### Étape 2 : Activez l’environnement virtuel Python :

```
source .venv/bin/activate
```

Vous saurez que l'environnement est activé si vous voyez (.venv) dans l'invite de commande.

##  3. Vérifier l'état du GPU

1. Tester si PyTorch détecte le GPU :

```
python -c "import torch; print(torch.cuda.is_available())"
```

2. Affichez le nom du GPU détecté :

```
python -c "import torch; print(torch.cuda.get_device_name(0))"
```

Résultat attendu pour la config:
```
True
<nom du gpu>
```

##  4. Désactiver l’environnement virtuel

Lorsque vous avez terminé votre session de travail :

1. Désactivez l’environnement virtuel :

```
deactivate
```

2. Quittez WSL :

```
exit
```

3. Arrêtez WSL pour libérer les ressources :

```
wsl --shutdown
```











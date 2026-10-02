# Egaliseur Systeme (alternative a Equalizer APO)

## Ce que c'est
Un egaliseur audio 10 bandes qui traite **tout le son de ton PC** (musique,
navigateur, jeux, etc.), sans passer par un pilote audio bas niveau.

Contrairement a Equalizer APO (qui s'installe dans le pilote Windows), ce
programme fonctionne en espace utilisateur : il capture le son via un cable
audio virtuel, l'egalise, et le renvoie vers tes haut-parleurs.

**Important — a lire :** ce binaire a ete compile pour Windows depuis un
environnement Linux (cross-compilation MinGW-w64). Il produit un vrai
`.exe` Windows valide, mais je n'ai pas pu le tester sur une vraie carte
son Windows. Si un souci apparait au premier lancement, dis-le moi et je
corrige.

## Installation (a faire une seule fois)

1. **Installe un cable audio virtuel gratuit** : VB-CABLE
   https://vb-audio.com/Cable/ (telecharge, installe, redemarre si demande).

2. **Regle la sortie audio par defaut de Windows** sur `CABLE Input (VB-Audio Virtual Cable)`
   (clic droit sur l'icone haut-parleur en bas a droite -> Parametres de son
   -> choisir la sortie).

3. Place `EqualiseurSysteme.exe` et `config.txt` dans le meme dossier.

4. Ouvre une invite de commandes dans ce dossier et lance :
   ```
   EqualiseurSysteme.exe --list
   ```
   Note les index affiches, par exemple :
   ```
   [0] CABLE Output (VB-Audio Virtual Cable)
   [1] Haut-parleurs (Realtek High Definition Audio)
   ```

5. Ouvre `config.txt` et renseigne :
   ```
   InputDevice=0     <- l'index du CABLE Output
   OutputDevice=1    <- l'index de tes vrais haut-parleurs/casque
   ```

6. Relance simplement :
   ```
   EqualiseurSysteme.exe
   ```
   Le son du PC passe maintenant par l'egaliseur.

## Regler l'egaliseur

Modifie les lignes `Band=` dans `config.txt` :
```
Band=1000   3.0   1.4
```
= bande a 1000 Hz, gain +3 dB, largeur Q=1.4.

Enregistre le fichier : le programme le recharge automatiquement en
quelques centaines de ms, sans coupure de son (comme Equalizer APO).

Ajuste `PreampDB` (negatif, ex: -3.0) si le son sature apres avoir monte
des bandes.

## Lancer au demarrage de Windows (optionnel)
Cree un raccourci vers `EqualiseurSysteme.exe` dans le dossier :
`Win+R` -> `shell:startup`

## Limites connues de cette version
- Pas d'interface graphique (fichier texte + console) — je peux en ajouter une si tu veux.
- Filtre uniquement de type "peaking" (comme un EQ graphique classique),
  pas les filtres shelf/passe-bas/passe-haut d'Equalizer APO.
- Resampling simple (lineaire) si les frequences d'echantillonnage du
  cable et des haut-parleurs different — qualite suffisante mais pas
  audiophile.
- Necessite VB-CABLE (logiciel tiers gratuit) car Windows ne permet pas
  d'intercepter le son systeme sans pilote virtuel ou sans APO enregistre.

## Recompiler soi-meme (optionnel)
Le code source complet est dans `src/`. Voir `BUILD.md`.

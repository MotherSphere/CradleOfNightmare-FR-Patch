# Cradle of Nightmare — Patch Français

Traduction française non-officielle de **Cradle of Nightmare: Flowers to you** (红锈雨 / *Hóng Xiù Yǔ*), un RPG de dark fantasy chinois développé sur RPG Maker VX Ace, disponible sur Steam ([App 3469850](https://store.steampowered.com/app/3469850/)).

> *Dans un monde devenu fou, le sang et la rouille pleuvent. Rappelle-toi.*

---

## État de la traduction

| Composant | Couverture | Détails |
|---|---|---|
| **Fichiers de données** (`.rvdata2`) | **100 %** | 19 485 / 19 485 chaînes uniques — 34 211 entrées patchées (maps, dialogues, items, skills, system, etc.) |
| **Scripts Ruby** (`Scripts.rvdata2`) | **~63 %** | 1 048 lignes patchées sur 1 653 candidates (menus, options, libellés UI hardcodés) |
| **Total approximatif du texte visible** | **~98 %** | Quelques lignes scripts non-patchées à cause de chaînes dynamiques ou d'échappements Ruby complexes |

Le jeu est **entièrement jouable en français** : menus, dialogues, items, compétences, options, interface de sauvegarde, écran de statut, etc.

---

## Installation

### Prérequis
- Posséder le jeu sur Steam : https://store.steampowered.com/app/3469850/
- Aucun autre patch n'est requis — tout est inclus (FR + correctifs runtime de SaiCateDoan).

### Étapes

1. **Localise le dossier d'installation Steam** :
   - Windows : `C:\Program Files (x86)\Steam\steamapps\common\CRADLE OF NIGHTMARE\`
   - Linux (Proton) : `~/.steam/steam/steamapps/common/CRADLE OF NIGHTMARE/`

2. **(Recommandé)** Sauvegarde le dossier `Data/` existant :
   ```
   Data/  ->  Data.backup/
   ```

3. **Télécharge ce repo** (`Code` > `Download ZIP`) ou clone-le :
   ```bash
   git clone https://github.com/MotherSphere/CradleOfNightmare-FR-Patch.git
   ```

4. **Copie tout le contenu du dossier** directement dans le dossier d'installation du jeu, en écrasant les fichiers existants quand demandé.

5. **Lance le jeu via Steam** normalement. Aucun exe alternatif à lancer.

### Désinstallation

Steam → clic droit sur le jeu → *Propriétés* → *Fichiers installés* → **Vérifier l'intégrité des fichiers du jeu**. Steam re-téléchargera les fichiers chinois originaux.

---

## Contenu du patch

| Fichier | Rôle |
|---|---|
| `Data/*.rvdata2` | 470 fichiers de données traduits en français (maps, events, items, etc.) |
| `System/RGSS300NEW.dll` | Runtime patcher de SaiCateDoan (corrige crashes, fuites mémoire) |
| `Game.exe` | Exécutable patché par SaiCateDoan (nécessaire au runtime modifié) |
| `Game.ini` | Config des polices (pointe vers `Roboto-Regular.ttf`) |
| `patches.json` | Patches runtime (appliqués par Joiplay sur Android ; ignoré sur Windows) |
| `Roboto-Regular.ttf` | Police compatible accents FR/EN |
| `LISEZ-MOI.txt` | Notice d'installation résumée |

---

## Style de traduction

- **Français courant**, pas de calques chinois ou anglais maladroits.
- **Tutoiement / vouvoiement contextuel** : *tu* pour l'intime, le familier, les pensées intérieures ; *vous* pour les étrangers et le formel.
- **Dark fantasy adulte** assumé — la traduction ne lisse pas le ton cru ou les thèmes dérangeants du texte original.
- **Noms chinois romanisés** conservés tels quels : Le Qing, Fang Yu, Hui Tuan, Yue Qing, etc.
- **Guillemets français** « » lorsque la source utilise `" "`.
- **Codes d'échappement** RPG Maker VX Ace préservés (`\C[N]`, `\V[N]`, `\N[N]`, `\I[N]`, etc.).

---

## Notes techniques (pour les curieux)

Le patch combine trois types de modifications :

1. **Données RPG Maker** (`.rvdata2` hors `Scripts.rvdata2`)
   Extraction via `rubymarshal` → traduction ligne par ligne → réinjection en préservant les attributs d'encodage et les codes d'échappement.

2. **Code Ruby** (`Scripts.rvdata2`)
   Décompression zlib de chaque script → extraction heuristique des chaînes UI (CN hanzi + EN sentences dans des constantes `UPPERCASE_NAME = "..."` ou appels `add_command(...)`) → substitution du littéral avec sa traduction **en conservant la ligne complète** pour éviter toute collision avec des identifiants homonymes → recompression.

3. **Vocab système**
   Le terme `@terms:@basic:1` (abréviation du niveau) est corrigé de `"ALOL"` vers `"Niv"`.

> ⚠️ **Découverte importante :** `patches.json` **n'est lu que par Joiplay** (émulateur Android). Sur Windows, `RGSS300NEW.dll` l'ignore complètement. Pour traduire les scripts, il faut donc modifier `Scripts.rvdata2` directement (ce que fait ce patch).

---

## Crédits

- **Jeu original** : développé par l'équipe chinoise de *Cradle of Nightmare: Flowers to you* (红锈雨)
- **Patch anglais partiel** ([référence secondaire](https://store.steampowered.com/app/3469850/)) : **Aprela EL**
- **Runtime patcher** (`Game.exe`, `RGSS300NEW.dll`, `patches.json`, fix polices) : **SaiCateDoan**
- **Traduction française et outillage de pipeline** : **[MotherSphere](https://github.com/MotherSphere)** (2026-04)

---

## Problèmes connus

- ~605 lignes de `Scripts.rvdata2` non-patchées (échappements Ruby complexes que notre matcher naïf ne gère pas).
- Les chaînes dynamiques type `"Memory #{i}"` ou concaténations runtime ne sont pas capturées — les numéros d'emplacements de sauvegarde peuvent rester en anglais.
- Quelques expressions idiomatiques chinoises ont été adaptées librement faute d'équivalent direct.

Pour signaler un problème de traduction, ouvre une [issue](https://github.com/MotherSphere/CradleOfNightmare-FR-Patch/issues) avec :
- Une capture d'écran
- Le contexte (map, PNJ, menu, etc.)
- La traduction suggérée si tu en as une

---

## Licence & avertissement

Ce patch est un **travail fan non-officiel**, fourni **TEL QUEL**, **sans garantie** et **sans aucun lien** avec les développeurs du jeu, Steam, Aprela EL ou SaiCateDoan.

Il est destiné à un usage **personnel** par les possesseurs légitimes du jeu sur Steam. Il ne contient, ne redistribue ni ne contourne aucun DRM — les fichiers fournis sont ceux qui doivent remplacer/coexister avec une installation légale du jeu.

Si tu es un ayant-droit du jeu original et souhaites le retrait du repo, ouvre une issue ou contacte directement [MotherSphere](https://github.com/MotherSphere).

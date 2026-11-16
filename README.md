[![Academic Year](https://img.shields.io/badge/Epitech-Tek1-blue?style=for-the-badge&logo=epitech&logoColor=white)](https://www.epitech.eu/)
[![Language: C](https://img.shields.io/badge/Language-C-00599C.svg?style=for-the-badge&logo=c)](https://en.wikipedia.org/wiki/C_(programming_language))
[![Module](https://img.shields.io/badge/Module-B--CPE--200-informational?style=for-the-badge)](#)

# 🤖 RobotFactory — Assembleur Corewar (ASM)

**RobotFactory** est le compilateur / assembleur officiel du projet **Corewar**. Son rôle est de traduire des programmes champions rédigés en langage d'assemblage Corewar (`.s`) en exécutables binaires de bytecode (`.cor`) conformes aux spécifications de la machine virtuelle Corewar.

---

## ⚙️ Architecture & Fonctionnalités

- **Parsing Lexical & Syntaxique** :
  - Extraction et validation des métadonnées du champion : `.name` (max `PROG_NAME_LENGTH` octets) et `.comment` (max `COMMENT_LENGTH` octets).
  - Traitement des commentaires (symboles `#` ou `;`), suppression des espaces superflus et gestion des sauts de ligne.
- **Encodage des Instructions** :
  - Reconnaissance des 16 mnémoniques du jeu d'instructions Corewar (`live`, `ld`, `st`, `add`, `sub`, `and`, `or`, `xor`, `zjmp`, `ldi`, `sti`, `fork`, `lld`, `lldi`, `lfork`, `aff`).
  - Calcul dynamique de l'octet de codage (*Coding Byte / CB*) déterminant le type des paramètres :
    - Registre : `REG_CODE` (`01`b)
    - Direct : `DIR_CODE` (`10`b)
    - Indirect : `IND_CODE` (`11`b)
- **Génération du Binaire `.cor`** :
  - Écriture de l'en-tête `header_t` avec conversion en Big-Endian du magic number `COREWAR_EXEC_MAGIC` (`0xea83f3`).
  - Calcul et injection de la taille exacte du bytecode (`prog_size`).
  - Sérialisation ordonnée des opcodes et de leurs arguments encodés.

---

## 🛠️ Compilation du Projet

```bash
make        # Génère l'exécutable 'asm'
make clean  # Nettoie les fichiers objets (.o)
make fclean # Supprime les fichiers objets et l'exécutable
make re     # Recompile l'ensemble
```

---

## 💻 Utilisation

```bash
./asm <champion.s>
```

### Exemple :
```bash
./asm tests/abel.s
# Génère le binaire exécutable 'abel.cor'
```

Si le fichier source contient une erreur de syntaxe ou une instruction inconnue, `asm` affiche un message explicite sur la sortie d'erreur et quitte avec le code d'erreur `84`.

{\rtf1\ansi\ansicpg1252\cocoartf2870
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\paperw11900\paperh16840\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 # Provenance des donn\'e9es\
\
Ces donn\'e9es proviennent du projet OncoLake original, r\'e9alis\'e9 en bin\'f4me \
en 2024-2025 dans le cadre du cours \'e0 EFREI.\
\
## Repo source\
- URL : https://github.com/SDK-Bmd/Oncolake\
- Contributeur (moi) : Florian  DELSUC, en tant que bin\'f4me\
- Commit HEAD au moment de l'extraction : 740b93677b7be0350adf845f562a196fc8ec1fbe \
\
## Date d'extraction\
5 septembre 2026\
\
## Contenu extrait\
- `manifest.json` : 418 prot\'e9ines humaines (231 oncog\'e8nes KW-0656 + 187 \
  suppresseurs KW-0043, humain reviewed), telles qu'ing\'e9r\'e9es depuis \
  UniProt \'e0 la date de l'ingestion originale.\
- `cif_oncolake.zip` : 409 fichiers .cif AlphaFold correspondants \
  (414 prot\'e9ines avec structure - 5 dual-label = 409 fichiers uniques).\
- `features_baseline_ref.parquet` : features handcraft\'e9es calcul\'e9es par \
  la baseline originale (404 prot\'e9ines \'d7 25 features).\
- `metrics_baseline_ref.json` : m\'e9triques rapport\'e9es par la baseline \
  originale (CV accuracy = 0.5321, test = 0.4554, ne bat pas la baseline \
  majoritaire \'e0 0.5569).\
\
## Versions approximatives des sources externes\
- UniProt : release de l'\'e9poque de l'ingestion originale (date exacte \
  inconnue, \'e0 estimer d'apr\'e8s la date du dernier commit du repo source).\
- AlphaFold DB : version de production accessible via \
  https://alphafold.ebi.ac.uk \'e0 la m\'eame p\'e9riode.\
\
## Politique de non-r\'e9g\'e9n\'e9ration\
Ces donn\'e9es ne sont PAS r\'e9g\'e9n\'e9r\'e9es depuis UniProt/AlphaFold dans ce \
projet, pour garantir la comparabilit\'e9 stricte avec la baseline \
originale. Toute ex\'e9cution du pipeline OncoLake original aujourd'hui \
donnerait un dataset l\'e9g\'e8rement diff\'e9rent (UniProt et AFDB \'e9voluent \
en continu).}
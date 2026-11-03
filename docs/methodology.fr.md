<p align="right"><a href="methodology.md">English</a></p>

# Méthodologie — Ghana (2014–2025)

## Données et nettoyage

VIIRS DNB mensuel (VCMSLCFG) et annuel VNL V2, DMSP–VIIRS harmonisé, Black Marble quotidien, GHSL/WorldPop, Sentinel-5P NO₂/SO₂, MODIS LST, Banque mondiale. Nettoyage : pixels valides si cf_cvg ≥ 2, unité-mois gardée si ≥ 80 % de pixels observés, pics remplacés, fond et torchères masqués.

## 📈 Cas d'usage 1 — Dynamiques temporelles

- **Question** — L'activité accélère-t-elle ou ralentit-elle, hors effet de saison ?
- **Données** — VIIRS VCMSLCFG (monthly), VIIRS VNL V2 (annual), Harmonised DMSP–VIIRS (Li et al., 2020)
- **Méthode** — STL robuste (période 12) sur log(somme des lumières) ; pente de Theil–Sen et test de Mann–Kendall sur les composites annuels ; détection d'anomalies et de ruptures.
- **Validation** — Significativité de la tendance (Mann–Kendall) et cohérence mensuel/annuel (**p-value = < 0,0001**)
- **Incertitude** — IC 95 % de la croissance annuelle : +15,7 % à +18,5 %
- **Limites** — Couverture nuageuse et nuits courtes en été ; la lumière n'est pas la valeur ajoutée.
- **Statut** — `experimental` · Confiance: élevée
- **Références** — Cleveland et al. (1990) STL ; Sen (1968) ; Elvidge et al. (2017).
- **Page du tableau de bord** — [`#time`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/fr/?country=GHA#time)

**Résultats de cette exécution**

- `F02` Entre 2014 et 2025, la lumière nocturne de Ghana a évolué de +17,1 % par an (IC 95 % : +15,7 % à +18,5 %). Sur les 12 derniers mois, le niveau désaisonnalisé est +28,3 % par rapport aux 12 mois précédents. (confiance élevée : tendance significative (p < 0,01 ; n = 12))
- `F75` Validation : Significativité de la tendance (Mann–Kendall) et cohérence mensuel/annuel (p-value = < 0,0001). Incertitude : IC 95 % de la croissance annuelle : +15,7 % à +18,5 % Limites : Couverture nuageuse et nuits courtes en été ; la lumière n'est pas la valeur ajoutée. Statut : statistique expérimentale ; confiance élevée.

## 🗺️ Cas d'usage 2 — Croissance régionale et convergence

- **Question** — Quelles régions décollent, lesquelles décrochent ?
- **Données** — VIIRS VNL V2, GHSL / WorldPop, Sentinel-5P NO₂
- **Méthode** — Croissance robuste par unité (Theil–Sen, Mann–Kendall), classes croissance/stagnation/déclin, β- et σ-convergence, indice de Herfindahl.
- **Validation** — Corrélation de rang avec le NO₂ troposphérique (source indépendante) (**Spearman ρ = 0,25**)
- **Incertitude** — Classe attribuée seulement si |pente| ≥ seuil et p < α ; IC de β (erreurs robustes).
- **Limites** — Petites unités : bruit et débordement de lumière (blooming) entre voisins.
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Barro et Sala-i-Martin (1992) convergence ; Henderson, Storeygard et Weil (2012).
- **Page du tableau de bord** — [`#regions`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/fr/?country=GHA#regions)

**Résultats de cette exécution**

- `F03` Sur 260 unités ADM2, 260 sont en croissance significative, 0 stagnent et 0 déclinent. L'activité lumineuse reste concentrée : Greater Accra Region concentre 28 % de la lumière nationale. (confiance moyenne : classement sur 260 unités, seuil ±1 %/an et p < 0,10)
- `F04` Entre unités ADM2, la lumière par habitant converge : les unités les moins éclairées rattrapent leur retard. (confiance moyenne : β = −0,043 [−0,050 ; −0,035], n = 256)
- `F24` Greater Accra Region (ADM1, 2025) : part de la lumière nationale 27,5 %, croissance annuelle +14,3 % (IC +13,3 % à +15,7 %, classe Croissance), lumière par habitant 0,816, population 0,28 M, dans le noir 3 %, PIB estimé (expérimental) 21,83 Md USD.
- `F25` Ashanti Region (ADM1, 2025) : part de la lumière nationale 18,7 %, croissance annuelle +16,9 % (IC +16,0 % à +18,3 %, classe Croissance), lumière par habitant 0,406, population 0,38 M, dans le noir 1 %, PIB estimé (expérimental) 14,81 Md USD.

## 💹 Cas d'usage 3 — Relation lumières–PIB

- **Question** — Peut-on estimer la croissance avant sa publication, et le PIB régional ?
- **Données** — VIIRS, PIB réel (Banque mondiale, WDI)
- **Méthode** — log(lumière) ~ log(PIB) en niveaux et en croissance, MCO avec écarts-types HAC ; prévision hors échantillon ; PIB régional = PIB national réparti au prorata de la lumière.
- **Validation** — Suivi hors échantillon de la croissance officielle (**corrélation / EAM (points) = -0,43 / 2,6**)
- **Incertitude** — IC 95 % de l'élasticité : 3,34 à 3,67 ; intervalles de prévision 80 % et 95 %.
- **Limites** — Échantillon annuel court ; le PIB régional est une statistique expérimentale à confronter aux comptes régionaux.
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Henderson et al. (2012) AER ; Chen et Nordhaus (2011) PNAS ; Gibson et al. (2021) JDE.
- **Page du tableau de bord** — [`#time`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/fr/?country=GHA#time)

**Résultats de cette exécution**

- `F05` L'élasticité de la lumière au PIB réel est de 3,51 en niveaux (IC 95 % : 3,34 à 3,67, R² = 0,98, 12 années) et de 0,25 en taux de croissance (IC : −2,07 à 2,56). Hors échantillon, la croissance des lumières suit celle du PIB avec une corrélation de −0,43 (erreur absolue moyenne : 2,6 point de croissance). (confiance moyenne : relation nette mais seulement 12 années)
- `F43` Élasticité lumières–PIB réel en niveaux : β = 3,51 (IC 95 % 3,34 à 3,67, R² = 0,98, n = 12, confiance moyenne : relation nette mais seulement 12 années). +1 % de PIB ↔ +β % de lumière.
- `F44` Élasticité lumières–PIB réel en taux de croissance : β = 0,25 (IC 95 % -2,07 à 2,56, R² = 0,00, n = 11, confiance faible : n = 11, non significatif (p = 0,83)). +1 % de PIB ↔ +β % de lumière.
- `F45` Élasticité lumières–PIB réel en série longue DMSP–VIIRS : β = 0,93 (IC 95 % 0,71 à 1,16, R² = 0,92, n = 30, confiance élevée : n = 30, p < 0,01, IC étroit). +1 % de PIB ↔ +β % de lumière.

## ⚡ Cas d'usage 4 — Chocs et résilience

- **Question** — Quelle a été la profondeur d'un choc, et la vitesse de récupération ?
- **Données** — VIIRS (monthly), Black Marble VNP46A2 (daily), catalogue d'événements
- **Méthode** — Écart au niveau d'avant-choc sur la série désaisonnalisée ; ruptures structurelles ; indice quotidien Black Marble.
- **Validation** — Le creux dépasse-t-il la variabilité ordinaire ? (**creux (choc principal) = 3,2 % — non**)
- **Incertitude** — Variabilité mensuelle d'avant-choc (écart-type robuste) ; ruptures inexpliquées signalées.
- **Limites** — Les chocs touchant des activités peu éclairées (agriculture, services de jour) sont sous-estimés.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Román et al. (2018) ; Elvidge et al. (2020) lumières et confinements.
- **Page du tableau de bord** — [`#shocks`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/fr/?country=GHA#shocks)

**Résultats de cette exécution**

- `F06` Le choc le plus marqué dans la série désaisonnalisée est « COVID-19 » : creux de +3,2 % (05/2020), retour au niveau d'avant-choc après 3 mois. (confiance faible : creux comparé à la variabilité mensuelle d'avant-choc)
- `F47` COVID-19 (2020-03-01 → 2021-06-30) : creux de 3,2 % le 2020-05-01, retour au niveau d'avant-choc après 3 mois. Distinct du bruit : non.
- `F48` Ruptures structurelles : 2015-09-01 (42,2 %); 2020-11-01 (15,6 %); 2023-08-01 (-9,9 %); 2024-08-01 (27,8 %). Sans événement connu à ±6 mois : 3.
- `F49` Régions les plus touchées (creux) : Northern Region -33,3 % (covid19), Greater Accra Region -15,6 % (covid19), Volta Region -10,4 % (covid19), Oti Region -8,7 % (covid19), Savannah Region -8,1 % (covid19).

## ⚖️ Cas d'usage 5 — Inégalités et électrification

- **Question** — Où vivent les populations privées d'électricité ?
- **Données** — VIIRS VNL V2, GHSL / WorldPop, GHSL SMOD, accès à l'électricité (WDI)
- **Méthode** — Gini et Theil pondérés par la population ; population des pixels habités sous le seuil de détection ; sensibilité à trois seuils ; IC bootstrap de la variation du Gini.
- **Validation** — Écart avec le taux d'accès à l'électricité de la Banque mondiale (**écart moyen (points) = 10,8**)
- **Incertitude** — Plage selon le seuil de radiance ; IC bootstrap du Gini.
- **Limites** — Proxy de l'éclairage extérieur, pas du raccordement : un foyer raccordé mais peu éclairé paraît « dans le noir ».
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Theil (1967) ; Falchetta et al. (2020) accès à l'électricité par les lumières.
- **Page du tableau de bord** — [`#inequality`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/fr/?country=GHA#inequality)

**Résultats de cette exécution**

- `F07` Le Gini de la lumière par habitant (ADM2) vaut 0,38 en 2025 (baisse significative depuis 2014). Environ 0,03 million(s) de personnes vivent dans des zones habitées sans lumière détectable (2 % de la population habitée). (confiance moyenne : sensible au seuil de radiance (de 0,03 à 0,06 M selon le seuil) ; proxy d'éclairage extérieur, pas de raccordement)
- `F50` Gini de la lumière par habitant (ADM2) : 0,470 en 2014 → 0,381 en 2025 (variation -0,090, IC bootstrap -0,134 à -0,047). Theil T 0,258 ; part entre régions 20 %.
- `F51` Habitants de zones habitées sans lumière détectable : 0,18 M (15 %) en 2014 → 0,03 M (2 %) en 2025. Rapport lumière/hab. urbain/rural 0,4. Proxy de l'accès à l'électricité, sensible au seuil.
- `F52` Écart moyen entre la part de la population en zone éclairée et le taux d'accès à l'électricité de la Banque mondiale : 10,8 points.

## 🏭 Cas d'usage 6 — Zones industrielles

- **Question** — Où est l'industrie, et son activité progresse-t-elle ?
- **Données** — VIIRS VNL V2, GHSL BUILT-S, Sentinel-5P NO₂/SO₂, MODIS MOD11A2, OpenStreetMap
- **Méthode** — Concordance de six signaux par pixel (≥ 3 dont la lumière), grappes 8-connexes, typologie et confiance.
- **Validation** — Comparaison avec la liste de référence (OpenStreetMap) (**précision / rappel / F1 = 17 % / 31 % / 0,22**)
- **Incertitude** — Confiance par grappe selon le nombre de signaux forts ; sites isolés à vérifier.
- **Limites** — Résolution de Sentinel-5P (≈ 5 km) et MODIS (1 km) : les signaux qualifient un voisinage.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Elvidge et al. (2016) torchères ; Pesaresi et al. (2023) GHSL.
- **Page du tableau de bord** — [`#industry`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/fr/?country=GHA#industry)

**Résultats de cette exécution**

- `F08` 210 grappes industrielles détectées par concordance de signaux satellitaires : 60 d'industrie lourde, 13 zones d'activités et de logistique, 11 sites d'hydrocarbures et 126 sites isolés à vérifier. Elles émettent 14,7 % de la lumière nationale (dernière année) ; leur lumière évolue de +14,6 % par an. Ashanti Region concentre la plus forte activité industrielle. (confiance faible : précision 17 % et rappel 31 % face à la liste de référence)
- `F53` 210 grappes industrielles (≥ 3 signaux sur 6) : Site isolé à vérifier 126, Industrie lourde 60, Zone d'activités et logistique 13, Hydrocarbures et torchères 11. Part de la lumière nationale : 14,7 % ; croissance annuelle +14,6 %. Validation (OpenStreetMap) : précision 17 %, rappel 31 %.
- `F54` IND-001 — Site isolé à vérifier à Oforikrom Municipal (Ashanti Region) (599.205 km², 3 signaux, confiance faible); IND-002 — Industrie lourde à Sagnerigu (Northern Region) (287.885 km², 4 signaux, confiance moyenne); IND-004 — Site isolé à vérifier à Ho Municipal (Volta Region) (72.67 km², 3 signaux, confiance faible); IND-003 — Industrie lourde à Bolgatanga Municipal (Upper East Region) (74.605 km², 4 signaux, confiance moyenne); IND-012 — Zone d'activités et logistique à Kpone Katamanso (Greater Accra Region) (22.79 km², 3 signaux, confiance faible); IND-009 — Site isolé à vérifier à Yendi Municipal (Northern Region) (27.305 km², 3 signaux, confiance faible); IND-005 — Site isolé à vérifier à Asante Akim Central Municipal (Ashanti Region) (33.755 km², 3 signaux, confiance faible); IND-011 — Industrie lourde à Wa Municipal (Upper West Region) (25.37 km², 3 signaux, confiance faible); IND-008 — Site isolé à vérifier à Sekyere East (Ashanti Region) (28.38 km², 3 signaux, confiance faible); IND-006 — Site isolé à vérifier à Hohoe Municipal (Volta Region) (30.96 km², 3 signaux, confiance faible)
- `F55` Ashanti Region : 37 grappe(s) industrielle(s), 780,7 km², 41,2 % de la lumière de la région.

## 🏖️ Cas d'usage 7 — Tourisme saisonnier

- **Question** — Quelles zones vivent du tourisme, et comment évolue la saison ?
- **Données** — VIIRS (monthly), nuitées ou arrivées WDI
- **Méthode** — Surcroît estival net des unités comparables de même latitude ; test unilatéral ; indice de saison base 100 ; saisons recoupant le Ramadan signalées.
- **Validation** — Corrélation avec les nuitées (**r = non disponible**)
- **Incertitude** — p-valeur par unité ; années 2020–2021 exclues du classement.
- **Limites** — Toute activité estivale (diaspora, résidences secondaires, festivals) est captée, pas seulement le tourisme.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Analyses saisonnières des lumières et du tourisme, par ex. Hu et al. (2021).
- **Page du tableau de bord** — [`#tourism`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/fr/?country=GHA#tourism)

**Résultats de cette exécution**

- `F09` 62 unités sur 260 ont un surcroît de lumière estival net d'au moins 10 % : Sekyere Afram Plains North (Ashanti Region), Wa Municipal (Upper West Region), Ejura-sekyedumase (Ashanti Region), Ketu South (Volta Region). Le surcroît net médian atteint +26 % dans la zone la plus touristique. L'indice de saison (base 100 = 2019) tombe à 44 en 2020 et vaut 286 en 2025. (confiance faible : aucune statistique de nuitées pour valider l'indicateur)
- `F68` 62 zone(s) touristique(s) sur 260 unités ADM2 (surcroît estival net ≥ 10 %, mois de pointe [7, 8]) : Sekyere Afram Plains North (Ashanti Region) (+26 %, confiance élevée), Wa Municipal (Upper West Region) (+26 %, confiance élevée), Ejura-sekyedumase (Ashanti Region) (+25 %, confiance élevée), Ketu South (Volta Region) (+22 %, confiance élevée), Sagnerigu (Northern Region) (+22 %, confiance élevée), Tema West Municipal (Greater Accra Region) (+22 %, confiance élevée), Kpone Katamanso (Greater Accra Region) (+20 %, confiance élevée), Atebubu Amantin (Bono East Region) (+20 %, confiance élevée), Tamale Metropolitan (Northern Region) (+19 %, confiance élevée), Weija Gbawe Municipal (Greater Accra Region) (+19 %, confiance élevée).
- `F69` Indice de saison (base 100 = 2019) : 2014 : 45, 2015 : 44, 2016 : 54, 2017 : 79, 2018 : 14, 2019 : 100, 2020 : 44, 2021 : 33, 2022 : 81, 2023 : 307, 2024 : 111, 2025 : 286. Années avec Ramadan chevauchant la saison : 2014, 2015, 2018, 2019, 2020, 2021, 2022, 2023.
- `F81` Validation : Corrélation avec les nuitées (r = non disponible). Incertitude : p-valeur par unité ; années 2020–2021 exclues du classement. Limites : Toute activité estivale (diaspora, résidences secondaires, festivals) est captée, pas seulement le tourisme. Statut : statistique expérimentale ; confiance faible.

## 🏙️ Cas d'usage 8 — Signaux d'urbanisation

- **Question** — Où les villes s'étendent-elles, où les villages s'électrifient-ils, et où la population croît-elle sans lumière ?
- **Données** — VIIRS VNL V2, GHSL GHS-POP / WorldPop, GHSL GHS-BUILT-S R2023A, population urbaine (WDI)
- **Méthode** — Surface éclairée (pixels au-dessus du seuil) et population par unité ; croissances de Theil–Sen ; pixels nouvellement éclairés (sombres deux années de suite au début, éclairés deux années de suite à la fin), séparés entre électrification de zones habitées et nouvelles implantations ; typologie lumière/population.
- **Validation** — Corrélation de rang avec la croissance de la surface bâtie GHSL (source indépendante) (**Spearman ρ = 0,55**)
- **Incertitude** — Persistance exigée sur deux années pour limiter le bruit ; marge de ± 1 point entre croissances avant de classer.
- **Limites** — La lumière mesure l'éclairage extérieur, pas l'urbanisation au sens administratif ; le débordement (blooming) élargit les villes ; la population GHSL est interpolée entre époques.
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Zhou et al. (2015) étendue urbaine par les lumières ; Pesaresi et al. (2023) GHSL ; Min et al. (2013) électrification des villages.
- **Page du tableau de bord** — [`#urban`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/fr/?country=GHA#urban)

**Résultats de cette exécution**

- `F70` Surface éclairée nationale : +17,1 % par an ; population : +2,1 % par an. Classes (ADM2) : Urbanisation électrifiée 223, Croissance non éclairée 33, Croissance équilibrée 2, Indéterminé 1, Stable ou en déclin 1.
- `F71` Entre 2014 et 2025 : 32 028 km² nouvellement éclairés, dont 1 685 km² de zones déjà habitées (électrification, ≈ 131 k habitants) et 30 343 km² de nouvelles implantations ; 2 km² ont perdu leur lumière.
- `F72` Plus forte extension de la surface éclairée : East Gonja Municipal (Savannah Region) (+84,6 %/an), Yunyoo-nasuan (North East Region) (+47,0 %/an), Bongo (Upper East Region) (+44,2 %/an), Tempane (Upper East Region) (+44,0 %/an), Nanton (Northern Region) (+39,8 %/an), Krachi Nchumuru (Oti Region) (+38,3 %/an). Croissance non éclairée (population plus rapide que la lumière) : Adenta Municipal (Greater Accra Region), Ledzokuku Municipal (Greater Accra Region), La Dade-kotopon (Greater Accra Region), La-nkwantanang-madina (Greater Accra Region), Ga East (Greater Accra Region), Ayawaso West (Greater Accra Region), Ga Central Municipal (Greater Accra Region), Kwabre East (Ashanti Region).
- `F73` Corrélation de rang (Spearman) entre croissance de la surface éclairée et croissance du bâti GHSL : 0,55 (p = 0,000, 260 unités).

## Limites générales des lumières nocturnes

- **Ce que mesurent les lumières** — Radiance émise vers le haut vers 01 h 30 : l'agriculture, le commerce de jour, les services peu éclairés et l'économie informelle rurale sont mal captés.
- **Saturation et débordement** — DMSP sature au centre des villes (DN 63) et « déborde » (blooming) ; VIIRS est bien meilleur mais le débordement gonfle encore la surface éclairée des villes.
- **Torchères et sites isolés** — Le masque automatique peut retirer des mines, ports ou centrales isolés, et manquer de petites torchères ; les candidats sont exportés pour vérification.
- **Nuages, saisons, lune** — Les mois nuageux sont partiellement observés ; la STL retire la saisonnalité moyenne mais pas une saison anormale (neige, mousson tardive).
- **Ruptures de produit** — DMSP et VIIRS ne sont pas directement comparables : la série longue harmonisée (Li et al., 2020) est un produit modélisé, à lire en tendance seulement.
- **Élasticité NTL–PIB** — Estimée sur 10 à 30 points annuels : intervalles larges, instabilité possible, relation non causale et variable selon le niveau de développement.
- **Accès à l'électricité** — « Habité sans lumière » ≠ « non raccordé » : un foyer raccordé à faible consommation est invisible ; l'indicateur dépend fortement du seuil de radiance et de la population.
- **Limites administratives** — geoBoundaries/GAUL peuvent différer des limites officielles ; les petites unités ADM2 sont sensibles au débordement de la lumière des voisines.
- **Zones industrielles** — La détection repose sur des seuils : une centrale, un port ou un grand centre commercial peut cumuler les signaux ; une usine peu éclairée ou sans émissions visibles échappe à la détection. Sentinel-5P (≈ 5 km) et MODIS (1 km) sont plus grossiers que VIIRS : les signaux NO₂/SO₂/chaleur qualifient un voisinage, pas un bâtiment.
- **Tourisme estival** — Le surcroît estival mesure toute hausse de lumière en été (résidences secondaires, diaspora, fêtes, chantiers), pas seulement le tourisme ; aux hautes latitudes, les nuits d'été très courtes réduisent les observations VIIRS. Le Ramadan modifie l'activité nocturne : les étés concernés sont signalés.
- **Urbanisation** — La surface éclairée dépend du seuil de détection et du débordement de lumière (blooming) autour des villes ; un quartier raccordé mais peu éclairé reste invisible. La population (GHSL/WorldPop) est modélisée à partir des recensements : sa croissance n'est pas une observation indépendante, et les années entre deux millésimes sont interpolées.


---
<sub>Généré par le notebook le 2026-11-03 · version 2.1.0</sub>

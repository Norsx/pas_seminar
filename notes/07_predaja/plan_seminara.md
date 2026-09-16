---
id: PLAN_SEMINARA
type: plan
updated: 2026-09-16
---
# Plan seminara (radni plan — prati se i ažurira)

> Zamjenjuje tablicu poglavlja iz [[seminar_mapa]] (ta je pisana 13. 9., prije završene misije).
> Svaki agent koji piše seminar **mora pročitati cijeli ovaj fajl** prije rada.

## 0. Zadatak (od korisnika, 16. 9. 2026.)

- Napisati seminar **u ime Ivana Noršića**, kolegij *Projektiranje autonomnih sustava*.
- Profesor traži u seminaru: **slike**, **nacrt arhitekture**, **link na GitHub s lijepim
  README-om** i **kodove**.
- **Druga stranica** (odmah iza naslovnice): naslov *GitHub repozitorij cijelog projekta*, ispod
  link **https://github.com/KxHartl/PAS-DUAL-ARM**, ispod *Izradili: Krešimir Hartl i Ivan Noršić* (tim redoslijedom; na naslovnici je autor samo Ivan Noršić).
- Seminar mora imati **puno slika**. Korisnik daje snimke zaslona iz simulacije (popis u §4.2),
  ostale slike generiramo iz projekta (§4.1).
- Izvođači kolegija (naslovnica): izv. prof. dr. sc. Marko Švaco (P), doc. dr. sc. Bojan
  Šekoranja (P), Branimir Ćaran, mag. ing. mech. (V).

## 1. Tvrda pravila pisanja

1. **Ništa se ne izmišlja.** Svaka brojka, ime, tvrdnja i opis ponašanja mora postojati u kodu
   (`src/`, `scripts/`, `patches/`, `ros2.repos`) ili u projektnim dokumentima (`README.md`,
   `RUNNING.md`, `MAPPING.md`, `notes/`, `data/raw/zadatak/`). Ako se nešto ne može pronaći → ne
   piše se. Nema općeg znanja „iz glave“ (npr. povijest ROS-a, teorija SLAM-a koje projekt ne
   navodi).
2. **Nije površno i nije kopija README-a.** README kaže *što* i *kako pokrenuti*; seminar
   objašnjava *kako je građeno i zašto*: strukturu paketa, tok podataka (topici, akcije,
   servisi, TF), odgovornosti čvorova, odluke i njihove razloge, izmjerene rezultate.
3. **Izvor istine po prioritetu:** (1) kod, (2) `README.md` i `notes/00_MAPA.md` (16. 9.),
   (3) `notes/03_problemi/P-45_mission_integration.md` i M-redovi u `notes/05_povijest/runovi.md`,
   (4) ostale kartice. **Kartice S-01…S-10 i `odstupanja.md` su dijelom zastarjele** (npr. S-03
   navodi `DiffDriveController`, a `controllers.yaml` ima `MecanumDriveController`; S-01 navodi
   lidar s 360 zraka, a `robot.urdf.xacro` ima 1080). Kad se kartica i kod razlikuju — **vrijedi
   kod**, a razlika se ne spominje kao činjenica bez provjere.
4. **Iskrenost** ([[D-12_honesty_abort_over_fake]]): ograničenja i odstupanja pišu se činjenično
   (zahtjev → pokušano → izmjereno → uzrok → što je napravljeno umjesto toga).
5. Jezik teksta: **hrvatski**, stručno, u 1. licu množine („razvili smo“, „odabrali smo“).
   Imena topica, čvorova, datoteka i parametara u `\texttt{}`.
6. Brojke s jedinicama (`0{,}30~m` ili `siunitx` ako ga architect uključi), decimalni zarez u
   tekstu, točka u kodu.

## 2. Literatura

Samo izvori koje projekt **već navodi**, bez vanjskog pretraživanja:

| Ključ (prijedlog) | Izvor | Gdje je u projektu |
|---|---|---|
| `zadatak2025` | B. Ćaran, *Izrada simulacijskog modela DUAL ARM robota u Gazebo okruženju*, 30. 11. 2025. | `data/raw/zadatak/task_caran_2025-11-30.pdf` |
| `mail2026` | B. Ćaran, mail „Re: PAS - Dual arm robot - Podaci“, 4. 5. 2026. (+ prilog STL, slika) | citati u `notes/01_zahtjevi/izvori.md` |
| `omnibase`, `kortex`, `pantilt`, `realsense`, `arucoros` | upstream repozitoriji (autor, licenca, URL, pinani commit) | `ros2.repos`, `README.md` §9, `notes/07_predaja/vanjski_paketi.md` |
| alati | ROS 2 Humble, Gazebo Fortress, ros2_control, MoveIt 2, Nav2, slam_toolbox, OpenCV ArUco | samo ako URL/ime postoji u projektu (`grep`) |

BibTeX kao `@misc` s `howpublished = {\url{...}}` i `note` s commitom. Nema `\cite` ključa koji
nije u `docs/references.bib`.
*Napomena za QA:* `data/sources/` je namjerno prazan — izvori su repozitoriji i zadatak iz
`data/raw/`, ne znanstveni radovi (odluka korisnika: „ništa ne izmišljaj, sve mora biti u
projektu“).

## 3. Struktura dokumenta

**Opseg (korisnik, 16. 9.): tijelo ~20 stranica** (Uvod → Zaključak, sa slikama). Ne pretjerivati s
opisima, ali **ništa bitno ne preskočiti**: svaki podsustav mora biti objašnjen dovoljno da čitatelj
razumije *kako je napravljen*. Pravilo gustoće: umjesto proze → kompaktne tablice (parametri,
čvorovi, kontroleri, senzori); slike u parovima (`\dvijeslike`) ili nizovima; bez ponavljanja istog
podatka u dva poglavlja (referenca `\ref` umjesto ponavljanja).
Prednji dio (naslovnica, **str. 2 GitHub + autori**, sadržaj, popisi) i prilozi **ne ulaze** u 20 stranica.

| # | Datoteka | Poglavlje | ~str. | Sadržaj (obavezno, ništa ne preskočiti) | Glavni izvori | Slike |
|---|---|---|---|---|---|---|
| 1 | `01-uvod.tex` | UVOD | 1.5 | zadatak [ZAD] i konkretizacija iz [MAIL]; cilj misije; alati; zahtjevi R-01…R-20 u **jednoj kompaktnoj tablici** (zahtjev, izvor, gdje je riješen, status); pregled rada | `izvori.md`, `00_MAPA.md`, README uvod | G02 |
| 2 | `02-arhitektura.tex` | ARHITEKTURA SUSTAVA | 3 | **nacrt arhitekture** (slojevi Gazebo ↔ `ros_gz_bridge`/`ign_ros2_control` ↔ controller_manager ↔ MoveIt/Nav2 ↔ vlastiti čvorovi); tablica čvorova (paket, čvor, odgovornost, glavni ulazi/izlazi); TF lanac; hijerarhija launch datoteka; struktura repozitorija i 4 vlastita paketa; vanjski paketi (`ros2.repos`, pinani commitovi, 2 zakrpe); projektno okruženje (`run_native.sh`) | `src/*/launch/*.py`, `setup.py`, `bridge.yaml`, `ros2.repos`, `patches/`, S-10, README §8–9 | G04, G05, G06 |
| 3 | `03-model-i-okruzenje.tex` | MODEL ROBOTA I SIMULACIJSKO OKRUŽENJE | 3.5 | kompozicija `robot.urdf.xacro`; baza; torzo (STL B. Ćaran, montaža iz CAD mjera, hod, mase = procjena); 2× Gen3 + 2F-85; pan-tilt + D435; **tablica svih senzora** (tip, frekvencija, rezolucija/zrake, topic); DetachableJoint; poze ruku i izmjerene širine (tablica); svijet `seminar_world.sdf` (sobe, vrata, stolovi, kutija, markeri); `sim.launch.py` tijek u koracima | `robot.urdf.xacro`, `base/*.xacro`, `dual_arm_torso.urdf.xacro`, `postures.py`, S-01 (geometrija), `08_poze.md`, `seminar_world.sdf`, `sim.launch.py`, D-13, D-14 | G01, G08, K01, K02, K03, K04+K05 |
| 4 | `04-upravljanje.tex` | UPRAVLJANJE (ros2_control) | 1.5 | tablica 8 kontrolera (tip, zglobovi, sučelja); `mecanum_drive_controller` parametri; `position` vs `effort`+PID profil (D-21); lanac naredbi baze (`/cmd_vel` → collision monitor → `cmd_vel_relay` → kontroler) | `controllers.yaml`, `force_controllers.yaml`, `cmd_vel_relay.py`, `collision_monitor.yaml`, D-21, P-09 | G09 |
| 5 | `05-percepcija.tex` | PERCEPCIJA | 1.5 | `aruco_detector` (rječnik, veličina markera, PnP, izlazi); markeri kutije i stola; kamera glave i oblak točaka; kamere zapešća; mjerenje kutije i cross-check; `scan_filter`, `robot_extent`/`footprint_publisher` | `aruco_detector.py`, `main_task.py`, `scan_filter.py`, `robot_extent.py`, D-01, D-02, P-19, P-22 | K10+K12 (ili K11) |
| 6 | `06-navigacija.tex` | MAPIRANJE I NAVIGACIJA | 3 | SLAM (`mapping.launch.py`, `slam_params.yaml`, rezolucija, gate-ovi karte); AMCL; Nav2 (planer, upravljač, costmapovi); `feature_registry` (vrata/stolovi iz karte); `nav_zones` potencijalno polje (D-20); `room_navigator` (graf soba, portalne i dock poze, gate ruku, `navigate_through_poses`); dinamički obris (D-19); collision monitor; `nav_gui`; `loc_error` | `nav2.launch.py`, `mapping.launch.py`, `nav2_params.yaml`, `slam_params.yaml`, `feature_registry.py`, `nav_zones.py`, `room_navigator.py`, `footprint_publisher.py`, `MAPPING.md`, D-16, D-19, D-20, P-39, P-40 | G10+G11, K08+K09 |
| 7 | `07-manipulacija.tex` | MANIPULACIJA I DVORUČNI HVAT | 2.5 | MoveIt konfiguracija (SRDF grupe, kinematika, OMPL, kontroleri); zašto squeeze (85 mm vs 0.30 m); slijed STEP0–STEP7 iz koda (tablica: korak, što, provjera/abort); dokaz kontakta i attach; dizanje na vodilicama; gate-ovi poštenja | `pas_dual_arm_moveit_config/*`, `main_task.py` `run()`, `postures.py`, D-05, D-06, D-07, D-12, P-14, P-15, P-17 | K13–K17 (niz 2×2 ili 3+2) |
| 8 | `08-misija.tex` | ORKESTRACIJA MISIJE | 2 | `mission.launch.py`; 8 misijskih koraka; start (`/mission/start`, gumb); vožnja preko `room_navigator`-a; nošenje kroz vrata (referentna poza, gate); **odlaganje na marker u 11 koraka** s provjerama; očekivani log | `mission.launch.py`, `task.launch.py`, `main_task.py`, P-45, `misija.md` | G12, K18, K20–K22 (niz), K23 |
| 9 | `09-rezultati.tex` | REZULTATI, PROBLEMI I OGRANIČENJA | 2 | tablica izmjerenih rezultata (run 62, M1, M4, M5, `loc_error`, offline provjere); **tablica ključnih problema** (P-09, P-15, P-17, P-35/43, P-39, P-40, P-45, P-46: simptom → uzrok → rješenje, jedan red); trenutna provjerena ograničenja | `runovi.md`, P-kartice, README §10, `odstupanja.md` (provjeriti prema kodu) | — |
| 10 | `zakljucak.tex` | ZAKLJUČAK | 0.5 | što radi (izmjereno), što ne, naučeno (samo zapisano u projektu) | `00_MAPA.md`, P-45, `timeline.md` | — |
| A | `prilog-a-pokretanje.tex` | PRILOG A: POKRETANJE | ≤1 | preduvjeti, dohvat (`vcs import`, zakrpe), build, misija jednom naredbom | README §1–7, `RUNNING.md` | — |
| B | `prilog-b-kod.tex` | PRILOG B: IZVODI IZ KODA | ≤4 | **kodovi** — vidi §5 | kod | — |

## 4. Slike

Sve slike idu u `docs/figures/`. Architect osigurava makro koji umjesto **nepostojeće** slike
iscrta okvir s nazivom datoteke, pa se dokument prevodi i prije nego korisnik preda snimke.

### 4.1 Generiramo sami (G)

| ID | Datoteka | Što | Kako |
|---|---|---|---|
| G01 | `g01_torzo_cad_mjere.png` | CAD torza s mjerama (B. Ćaran) | kopija `data/raw/zadatak/torzo_cad_mjere.png` |
| G02 | `g02_ciljani_izgled.png` | ciljani izgled sustava iz maila | kopija `data/raw/zadatak/mail_img-000.png` |
| G03 | TikZ | stablo zahtjeva R0 → R1…R5 → R-01…R-21 | iz mermaid dijagrama u `00_MAPA.md` |
| G04 | TikZ | **nacrt arhitekture sustava** (slojevi, čvorovi, topici/akcije) | iz launch datoteka i koda |
| G05 | TikZ | hijerarhija launch datoteka i čvorova | `mission.launch.py` → `sim`/`nav2`/`task` |
| G06 | `dirtree`/verbatim | struktura repozitorija | `git ls-files` |
| G07 | `g07_urdf_stablo.pdf` | stablo linkova/zglobova (pojednostavljeno ili cijelo) | `urdf_to_graphviz` nad proširenim xacro-om |
| G08 | TikZ | tlocrt svijeta s koordinatama (sobe, vrata, stolovi, kutija, spawn) | brojke iz `seminar_world.sdf` |
| G09 | TikZ | tok naredbi baze i ruku | `cmd_vel_relay.py`, `collision_monitor.yaml`, `controllers.yaml` |
| G10 | `g10_karta.png` | SLAM karta `seminar_map.pgm` s mjerilom | Python iz `.pgm` + `.yaml` |
| G11 | `g11_zone.png` | zone/potencijalno polje, graf soba, poze | `scripts/check_zones.py --png` |
| G12 | TikZ | dijagram stanja misije (8 koraka + abort grane) | `main_task.py` |

### 4.2 Snimke zaslona od korisnika (K)

Korisnik sprema snimke u **`docs/figures/`** (ili `docs/figures/snimke/`) i sam ih imenuje opisno (ime govori što je na
slici). Ime u tablici je samo ciljni naziv: pri ubacivanju se snimka prepozna po imenu i sadržaju,
koristi pod svojim imenom (ili kopira pod ciljnim). **Neće stići sve** (korisnik): za svaku sliku koja ne
stigne odluči se ukloniti je ili zamijeniti generiranom — ne ostavljati okvir „SLIKA NEDOSTAJE“ u predaji. ★ = obavezno, ☆ = poželjno.

| ID | Datoteka | Što snimiti | Kako |
|---|---|---|---|
| K01 ★ | `k01_gazebo_robot.png` | Gazebo: cijeli robot izometrijski, odmah nakon spawna (raširene ruke) | `mission.launch.py`, prije pritiska gumba |
| K02 ★ | `k02_gazebo_poza_voznje.png` | Gazebo: robot sprijeda u pozi vožnje `DRIVE_V4` | isto, kad log javi `WAITING for the user` |
| K03 ★ | `k03_gazebo_svijet_odozgo.png` | Gazebo: cijeli svijet odozgo (3 sobe, 2 vrata, oba stola, kutija, robot) | pogled odozgo, odzumirati |
| K04 ★ | `k04_kutija_marker.png` | Gazebo: izbliza kutija s ArUco markerom na stolu u plavoj sobi | — |
| K05 ★ | `k05_stol_odlaganja.png` | Gazebo: izbliza stol u crvenoj sobi s markerom odlaganja | — |
| K06 ★ | `k06_rviz_tf.png` | RViz: model robota s uključenim TF okvirima | `display.launch.py` ili RViz misije, *TF* display |
| K07 ☆ | `k07_rviz_slam.png` | RViz: SLAM mapiranje u tijeku (djelomična karta) | `MAPPING.md` postupak |
| K08 ★ | `k08_rviz_navigacija.png` | RViz tijekom vožnje: karta, lidar, costmap, planirana putanja, obris robota | tijekom misije |
| K09 ★ | `k09_nav_gui.png` | prozor panela `nav_gui` s gumbom „MISIJA: po kutiju“ | tijekom misije |
| K10 ★ | `k10_kamera_marker.png` | slika kamere glave s vidljivim markerom kutije (+ TF `aruco_marker_frame` u RViz-u ako može) | RViz *Image* `/camera/image` |
| K11 ☆ | `k11_oblak_tocaka.png` | RViz: oblak točaka `/camera/points` na kutiji | RViz *PointCloud2* |
| K12 ☆ | `k12_kamera_zapesca.png` | slika kamere na zapešću prema bočnom markeru | RViz *Image* `/wrist_left/image` |
| K13 ★ | `k13_hvat_detekcija.png` | hvat 1/5: robot pred stolom u pozi `DETECTION_V4` | Gazebo |
| K14 ★ | `k14_hvat_prilaz.png` | hvat 2/5: `GRASP_V4`, jastučići pred bočnim plohama | Gazebo, izbliza |
| K15 ★ | `k15_hvat_kontakt.png` | hvat 3/5: oba jastučića na kutiji (stisak) | Gazebo, izbliza |
| K16 ★ | `k16_hvat_dizanje.png` | hvat 4/5: kutija podignuta (vodilice gore) | Gazebo |
| K17 ★ | `k17_nosenje.png` | hvat 5/5: robot s kutijom u pozi nošenja `CARRY_V4` | Gazebo |
| K18 ★ | `k18_vrata_s_kutijom.png` | Gazebo: robot s kutijom **u vratima** | Gazebo |
| K19 ☆ | `k19_rviz_vrata.png` | RViz u istom trenutku: putanja kroz vrata, costmap, obris | RViz |
| K20 ★ | `k20_odlaganje_prilaz.png` | odlaganje 1/3: robot pred stolom u crvenoj sobi | Gazebo |
| K21 ★ | `k21_odlaganje_spustanje.png` | odlaganje 2/3: kutija spuštena na marker, još u rukama | Gazebo, izbliza |
| K22 ★ | `k22_odlaganje_gotovo.png` | odlaganje 3/3: kutija na markeru, robot odmaknut | Gazebo |
| K23 ★ | `k23_log_misija.png` | terminal s retcima `PLACE VERIFIED` i `MISSION COMPLETE` | terminal misije |
| K24 ☆ | `k24_moveit_rviz.png` | MoveIt Motion Planning u RViz-u (obje ruke) | `moveit_rviz.launch.py` |
| K25 ☆ | `k25_rqt_graph.png` | `rqt_graph` tijekom misije | `rqt_graph` |
| K26 ☆ | `k26_kontroleri.png` | `ros2 control list_controllers` (svi aktivni) | terminal |

## 5. Kodovi (Prilog B)

Kratki izvodi (10–25 redaka), svaki s putanjom, rasponom redaka i 1–3 rečenice objašnjenja:
`robot.urdf.xacro` (kontaktni senzor + DetachableJoint), `controllers.yaml` (`base_controller`),
`mission.launch.py`, `main_task.py` (glavni slijed misije), `aruco_detector.py` (detekcija + PnP),
`nav_zones.py` (potencijalno polje), `room_navigator.py` (gate ruku), `main_task.py`
(`PLACE VERIFIED` provjera). Paket `listings`, naslov „Ispis“. U tijelu rada se na ispise
upućuje s `\ref`, kod se ne ponavlja u poglavljima.

## 6. Tijek rada i status

- [x] Analiza projekta, plan (ovaj fajl), `STATE.md`, metapodaci u `project.yaml`
- [x] Tectonic instaliran (`~/.local/bin/tectonic`)
- [ ] `latex_architect`: predložak, naslovnica s 3 izvođača, **str. 2 GitHub + autori**, popisi,
      `listings`, TikZ, makroi `\slika`/`\dvijeslike` s rezervnim okvirom, stubovi 10 poglavlja + 2 priloga, build
- [ ] Generirane slike G03 (izbačeno — zahtjevi su tablica), G04–G12
- [ ] `writer`: 1–3 (uvod, arhitektura, model i okruženje)
- [ ] `writer`: 4–6 (upravljanje, percepcija, navigacija)
- [ ] `writer`: 7–10 + prilozi (manipulacija, misija, rezultati, zaključak, pokretanje, kod)
- [ ] Build bez grešaka, tijelo ≈ 20 str. (`latex_surgeon` ako treba)
- [ ] `qa_reviewer` → `docs/REVIEW.md` (svaka tvrdnja ima izvor u projektu; ništa bitno preskočeno)
- [ ] Ispravci po recenziji
- [ ] Korisnik predao snimke u `docs/figures/snimke/` → ubaciti, provjeriti opise
- [ ] README: oba autora + link na `KxHartl/PAS-DUAL-ARM` (README u **tom** repou vidi profesor)
- [ ] Finalni build `--version v1.0`

# STATE

## Projekt

- **Naziv**: PAS-DUAL-ARM — Projektiranje i simulacija dvoručnog mobilnog manipulatora
- **Tip**: Seminar
- **Kolegij**: Projektiranje autonomnih sustava (FSB)
- **LaTeX format**: FSB Seminar
- **Izvođači**: izv. prof. dr. sc. Marko Švaco (P), doc. dr. sc. Bojan Šekoranja (P),
  Branimir Ćaran, mag. ing. mech. (V)
- **Autori projekta**: Ivan Noršić i Krešimir Hartl (seminar se predaje u ime Ivana Noršića)
- **GitHub (ide u seminar)**: https://github.com/KxHartl/PAS-DUAL-ARM

## Zadatak (korisnik, 16. 9. 2026.)

Napisati detaljan seminar o cijelom projektu. **Profesor traži u seminaru:**
1. slike (puno — korisnik daje snimke zaslona, ostale generiramo iz projekta),
2. nacrt arhitekture,
3. link na GitHub s lijepim README-om,
4. kodove.

Druga stranica, odmah iza naslovnice: naslov *GitHub repozitorij cijelog projekta*, link
`https://github.com/KxHartl/PAS-DUAL-ARM`, zatim *Izradili: Krešimir Hartl i Ivan Noršić*. Na naslovnici je autor (Student) samo **Ivan Noršić**.

## Trenutni fokus

- **Primopredaja za novog agenta: `notes/07_predaja/HANDOFF_seminar.md`** (čitati prvo).
- Plan i status rada: **`notes/07_predaja/plan_seminara.md`** (§6 checklista).
- Sljedeće: `latex_architect` postavlja `docs/`, zatim `writer` po poglavljima.
- **Opseg: tijelo ~20 stranica** (korisnik) — sažeto, ali ništa bitno ne preskočiti.

## Bilješke

- **Ništa se ne izmišlja** (korisnik): sve što seminar spominje mora postojati u kodu ili
  projektnim dokumentima. Literatura samo iz projekta (zadatak, mail, upstream repozitoriji).
- Seminar **ne smije biti površan ni kopija README-a** — objasniti strukturu, arhitekturu,
  tok podataka i odluke.
- Kartice `notes/02_rjesenja/S-*` i `odstupanja.md` su dijelom zastarjele; vrijedi kod.
- LaTeX: Tectonic u `~/.local/bin/tectonic`; build `./.ai/scripts/helpers/build-docs.sh`.

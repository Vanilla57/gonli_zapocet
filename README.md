
# Praktický zápočet — GIS Online (GONLI)

Krátká technická dokumentace pro jednoduchou jednosouborovou webovou mapovou aplikaci.

1) Popis projektu
- Jednoduchá webová mapová aplikace (single-file) implementovaná v `index.html` s Leaflet.js.
- Zobrazuje tři vrstvy ve společné kompozici:
	- Ortofoto ČR — WMS služba z ČÚZK.
	- Obce ORP — WMS z lokálního GeoServeru (http://localhost:8080); vrstva publikovaná ze shapefile, styl kategorizovaný podle ORP (Olomouc = zelený okraj, Prostějov = modrý okraj).
	- Komunikace — WFS z ArcGIS Online; data byla nahrána/uložena lokálně jako GeoJSON pro offline přístup.

2) Atributy a omezení
- Atributy prvků (např. `NAZEV`, `KODORP` pro obce; atributy komunikací) jsou načítány lokálně ze zdrojových souborů (`.shp`/GeoJSON) kvůli omezením CORS a nepředvídatelnému chování `GetFeatureInfo` u některých WMS.

3) Technologie a služby
- Frontend: vanilla HTML, CSS, JavaScript
- Mapová knihovna: Leaflet.js
- Vzdálené služby: ČÚZK WMS (orto), ArcGIS Online WFS
- Lokální služby: GeoServer (localhost:8080) pro WMS z shapefile

4) Struktura souborů (vybrané)
- `index.html` — hlavní jednosouborová aplikace
- `geojson_obce.geojson` — lokální kopie obcí/atributů
- `komunikace.geojson` / `komunikace_mikeska.gpkg` — komunikace (GeoJSON/GPKG)
- `zapocet_projekt.qgz` — QGIS projekt (volitelně)
- `zapocet2_styl.sld` — styl (SLD) použitý pro publikaci ve GeoServeru

5) Jak spustit
- Doporučeno spustit jako jednoduchý HTTP server (problémy s lokálním načítáním souborů a CORS):

```bash
python -m http.server 8000
# nebo (Windows PowerShell)
# py -m http.server 8000
```

- Pak otevřít v prohlížeči: `http://localhost:8000/index.html`.
- Alternativa: VS Code + Live Server extension.
- Poznámka: Pro plnou funkcionalitu musí běžet lokální GeoServer na `http://localhost:8080` s publikovanou vrstvou Obce ORP; bez něj bude vrstva z GeoServeru nepřístupná.

6) Zdrojová data
- Ortofoto: WMS — ČÚZK (oficiální WMS služba)
- Obce ORP: lokální shapefile publikovaný do GeoServeru (atributy: `NAZEV`, `KODORP`)
- Komunikace: GeoJSON (původně z ArcGIS Online WFS)

7) Poznámky ke sdílení / verzování
- Nepřidávejte do Gitu velké binární geoprostorové soubory (GPKG, shapefile přílohy). Použijte `.gitignore` (v repozitáři již přidáno).

Autor: MikeSka — Praktický zápočet KGI/GONLI, Palacký Univerzita Olomouc


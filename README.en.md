# China Village Boundaries Dataset

**[中文](README.md)** | English

## Overview

Village-level administrative boundary spatial data for all of mainland China, Hong Kong, and Macau in ESRI Shapefile format. Covers 33 provincial-level administrative divisions, 58 datasets, and 875,140 records.

## Data Source

- **Original sharer**: [@elpwc](https://x.com/elpwc/status/2064590494974591226) (shared via [cloud storage](https://x.com/elpwc/status/2064590494974591226))
- **Curator / re-uploader**: [@thedavidweng](https://x.com/thedavidweng)
- **Estimated time span**: Data collected between 2010–2022, mostly circa 2016
- **Origin**: Gathered from public internet sources. Exact provenance unknown. Some data may originate from China's Third National Land Survey and related government open data

## ⚠️ Usage Restrictions

- **Copyright/licensing status is unclear**. This dataset was collected from the internet; the original rights holder and license terms cannot be confirmed
- **Not claimed as "official" data**. Boundary accuracy and completeness have not been officially verified
- **Intended for personal research, academic analysis, and GIS learning only**
- **Not recommended for commercial use or as a legal/administrative reference**
- If you are the rights holder and believe this constitutes infringement, please contact for removal

## License

Released under **CC0 1.0** (Public Domain Dedication). The curator makes no claim to the original rights of the data, only waiving rights to the curation work.

> If you are the original rights holder and wish to adjust the license terms, please contact the curator.

## Data Format

- **Primary format**: ESRI Shapefile (.shp / .shx / .dbf / .prj / .cpg)
- **Secondary formats**: FileGDB (.gdb), GeoJSON, KML, GML (some provinces)
- **Encoding**: UTF-8 (majority) with known GBK/CP936 issues (see below)
- **CRS**: WGS84 (EPSG:4326) — unified across all 58 datasets

## Coordinate Reference System (CRS)

**Unified to WGS84 (EPSG:4326).** All 58 .shp files contain geographic coordinates (degrees). All .prj files declare WGS84.

> Original .prj files declared various CRS (CGCS2000, Krasovsky_1940_Albers, Hong_Kong_1980_Grid, etc.), but the .shp coordinate values were always geographic. See CHANGELOG.md for details.

## Field Encoding Notes

All 58 .cpg files declare **UTF-8** encoding. Most datasets have UTF-8 field names and values, with the following known issues:

**Mixed encoding datasets** (UTF-8 field names, GBK/CP936 field values):
- Hebei, Henan, Shaanxi: .cpg declares UTF-8 so field names are readable, but Chinese field values (village names etc.) are GBK

> GIS software will display field names correctly but Chinese field values may appear garbled. Fix with `ogr2ogr --config SHAPE_ENCODING GBK` to convert to GeoPackage.

**UTF-8 field names truncated by DBF 11-byte limit** (multiple provinces):
- Some .dbf files in Guangdong, Shanghai, Shanxi, Sichuan, Gansu, Zhejiang, Fujian, Heilongjiang, etc. have UTF-8 Chinese field names truncated by the DBF format's 11-byte field name limit
- Full field names have been recovered through byte-level analysis — see CHANGELOG.md

## Field Schema

Field structures vary across provinces. The complete field mapping table is in **[SCHEMA_MAPPING.md](SCHEMA_MAPPING.md)** (includes dry run validation results).

The mapping covers 11 core administrative hierarchy fields:

| Standard Field | Description | Coverage |
|---|---|---|
| `province_code` / `province_name` | Province level | 100% |
| `city_code` / `city_name` | Prefecture/city level | 100% |
| `county_code` / `county_name` | County/district level | 100% |
| `township_code` / `township_name` | Township level | 100% |
| `village_code` / `village_name` | Village level | 100% |
| `note` | Remarks | 100% |

> 52/58 datasets are fully mapped (90%). The remaining 6 have truncated UTF-8 Chinese field names from Shanghai's community management supplementary fields. Full names recovered via byte analysis — see CHANGELOG.md.

Common field name patterns (original names):

| Field Type | Common Original Names | Description |
|---|---|---|
| Admin code | `XZQDM`, `xzqdm`, `AREA_CODE`, `PAC`, `code` | 12-digit or 9-digit admin code |
| Admin name | `XZQMC`, `NAME`, `name`, `村名称`, `村级名` | Village/community name |
| Hierarchy codes | `省级码`, `市代码`, `区县码`, `乡镇码`, `村级码` | Multi-level admin codes |
| Hierarchy names | `省级名`, `市名`, `县区名`, `乡镇名`, `村名` | Multi-level admin names |
| Geometry | `SHAPE_Leng`, `SHAPE_Area` | Perimeter and area |

> Read with `dbfread`, `geopandas`, or QGIS directly.

## Directory Structure

```
china-village-boundaries/
├── 上海村界/          (2 datasets, with corrected version)
├── 云南村界/
├── 内蒙村界/          (2 datasets)
├── 北京村界/
├── 吉林村界/
├── 四川村界/
├── 天津村界/
├── 宁夏村界/
├── 安徽村界/
├── 山东村界/          (2 datasets)
├── 山西村界/
├── 广东村界/          (province-wide + Zhongshan/Huizhou/Suixi)
├── 广西村界/
├── 新疆村界/          (excluding Xinjiang Production & Construction Corps)
├── 江苏村界/
├── 江西村界/          (old + new version)
├── 河北村界/
├── 河南村界/
├── 浙江村界/          (2 versions)
├── 海南村界/
├── 湖北村界/
├── 湖南村界/
├── 澳门堂区统计区/    (admin districts + statistical zones + grid coords)
├── 甘肃村界/
├── 福建村界/
├── 西藏村界/
├── 贵州村界/
├── 辽宁村界/
├── 重庆村界/
├── 陕西村界/          (village + city/county/township auxiliary boundaries)
├── 青海村界/
├── 香港选区统计区单元区/(constituencies + statistical units + admin districts)
└── 黑龙江村界-林业局界/
    ├── 黑龙江省统计村界/ (with corrected version)
    └── 黑龙江森工集团/   (Daxing'anling/Longjiang/Yichun/Beidahuang)
```

## Province Data Summary

| Province | Records | CRS | Encoding Issues | DBF Date | Datasets |
|---|---|---|---|---|---|
| Shanghai | 20,111 | WGS84 | 11 field name truncations | 2023-04/07 | 3 |
| Yunnan | 13,595 | WGS84 | — | 2021-07 | 1 |
| Inner Mongolia | 29,140 | WGS84 | — | 2023-06/08 | 2 |
| Beijing | 8,021 | WGS84 | — | 2023-07 | 1 |
| Jilin | 10,194 | WGS84 | 7 field name truncations | 2024-03 | 1 |
| Sichuan | 41,297 | WGS84 | 8 field name truncations | 2023-07 | 1 |
| Tianjin | 5,847 | WGS84 | — | 2022-08 | 1 |
| Ningxia | 2,947 | WGS84 | 7 field name truncations | 2023-04 | 1 |
| Anhui | 17,848 | WGS84 | — | 2023-05 | 1 |
| Shandong | 171,758 | WGS84 | — | 2023-06/2024-03 | 2 |
| Shanxi | 30,778 | WGS84 | 10 field name truncations | 2024-03 | 1 |
| Guangdong | 28,323 | WGS84 | 8 field name truncations (province-wide) | 2023-05/2024-03 | 4 |
| Guangxi | 21,403 | WGS84 | — | 2023-05 | 1 |
| Xinjiang | 15,591 | WGS84 | — | 2023-12 | 1 |
| Jiangsu | 22,841 | WGS84 | — | 2023-04 | 1 |
| Jiangxi | 41,530 | WGS84 | — | 2023-06/2024-03 | 2 |
| Hebei | 58,399 | WGS84 | 8 field name truncations + **field values GBK** | 2024-04 | 1 |
| Henan | 50,371 | WGS84 | 8 field name truncations + **field values GBK** | 2022-08 | 1 |
| Zhejiang | 68,450 | WGS84 | 10 field name truncations | 2023-07/10 | 2 |
| Hainan | 4,822 | WGS84 | — | 2016-09 | 1 |
| Hubei | 32,457 | WGS84 | — | 2023-07 | 1 |
| Hunan | 31,238 | WGS84 | — | 2021-04 | 1 |
| Macau | 61 | WGS84 | — | 2022-11 | 3 |
| Gansu | 18,600 | WGS84 | 10 field name truncations | 2024-03 | 1 |
| Fujian | 19,760 | WGS84 | 8 field name truncations | 2024-03 | 1 |
| Tibet | 5,638 | WGS84 | — | 2024-03 | 1 |
| Guizhou | 19,267 | WGS84 | — | 2023-02 | 1 |
| Liaoning | 12,976 | WGS84 | 1 field name truncation | 2022-06 | 1 |
| Chongqing | 10,847 | WGS84 | — | 2023-05 | 1 |
| Shaanxi | 29,752 | WGS84 | **field values GBK** | 1995-2022 | 4 |
| Qinghai | 4,049 | WGS84 | — | 2023-03 | 1 |
| Hong Kong | 5,571 | WGS84 | — | 2022-05/11 | 4 |
| Heilongjiang | 21,298 | WGS84 | 9+1 field name truncations | 2023-05/12 | 9 |

## Known Issues

1. **~~CRS not unified~~**: CRS has been unified to WGS84 (EPSG:4326) — see CHANGELOG.md
2. **Field schema not unified**: Field naming and structure vary across provinces — mapping table established — see SCHEMA_MAPPING.md
3. **Zhejiang v3 deleted**: Versions 2 and 3 had identical .shp and .dbf (same MD5) — v3 removed
4. **Shanghai dataset field names truncated**: UTF-8 Chinese field names truncated by DBF 11-byte limit (not GBK corruption). Full names recovered via byte analysis — see CHANGELOG.md
5. **Shaanxi township .dbf date shows 1995**: Likely a DBF header date anomaly, not the actual data year
6. **Some provinces have multiple versions** (Inner Mongolia, Shandong, Jiangxi, Heilongjiang, Shanghai, Zhejiang)
7. **Xinjiang Production & Construction Corps not covered**: Current `新疆村界` only includes Xinjiang Uygur Autonomous Region data, not XPCC boundaries

## Usage

### QGIS
Drag and drop .shp files directly. QGIS reads .prj (CRS) and .cpg (encoding) automatically.

### Python (GeoPandas)
```python
import geopandas as gpd
gdf = gpd.read_file("path/to/file.shp")
print(gdf.crs)   # check CRS
print(gdf.head()) # preview fields
```

### Format Conversion
Use `ogr2ogr` to convert to GeoPackage (.gpkg) or other formats:
```bash
ogr2ogr -f GPKG output.gpkg input.shp  # CRS is already WGS84, no -t_srs needed
```

## Related Documents

- [SCHEMA_MAPPING.md](SCHEMA_MAPPING.md) — Field schema mapping table (with dry run validation)
- [CHANGELOG.md](CHANGELOG.md) — Full data preprocessing log (traceable)
- [metadata.json](metadata.json) — Structured metadata (33 provinces, 58 datasets, 875,140 records)

## Links

- Original tweet: https://x.com/elpwc/status/2064590494974591226
- GitHub Release (data download): https://github.com/thedavidweng/china-village-boundaries/releases/tag/v2026.06
- Zenodo DOI: [10.5281/zenodo.20664361](https://doi.org/10.5281/zenodo.20664361) (published via [zenodo-cli](https://github.com/thedavidweng/zenodo-cli))
- Internet Archive: https://archive.org/details/china-village-boundaries-2026

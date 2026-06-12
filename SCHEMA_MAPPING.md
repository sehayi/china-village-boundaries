# 字段 Schema 映射表 / Field Schema Mapping

## 统一目标字段

本映射表将各省 .dbf 中不统一的字段名映射到以下标准字段：

| 目标字段 | 说明 | 类型 |
|---|---|---|
| `province_code` | 省级行政区划代码 | C(12) |
| `province_name` | 省级行政区划名称 | C(100) |
| `city_code` | 地市级行政区划代码 | C(12) |
| `city_name` | 地市级行政区划名称 | C(100) |
| `county_code` | 区县级行政区划代码 | C(12) |
| `county_name` | 区县级行政区划名称 | C(100) |
| `township_code` | 乡镇级行政区划代码 | C(12) |
| `township_name` | 乡镇级行政区划名称 | C(100) |
| `village_code` | 村级行政区划代码 | C(12) |
| `village_name` | 村级行政区划名称 | C(100) |
| `note` | 备注 | C(254) |

## 港澳及特殊区域字段

| 目标字段 | 说明 | 适用范围 |
|---|---|---|
| `hk_district_name` | 香港区名 | 香港 |
| `hk_subunit` | 香港统计区单元 | 香港 |
| `hk_new_town` | 香港新市镇名 | 香港 |
| `macau_zone` | 澳门统计区编号 | 澳门 |
| `forestry_bureau` | 林业局名称 | 黑龙江 |
| `forestry_farm` | 林场名称 | 黑龙江 |
| `community_category` | 社区类别 | 上海 |
| `community_note` | 社区备注 | 上海 |
| `admin_level` | 行政层级标识 | 江西 |

## 完整映射关系

以下为每个目标字段对应的所有源字段名（按省份 .dbf 中的实际字段名）：

### province_code
`省代码`, `省级码`, `sheng`, `SHENG`

### province_name
`省级`, `省级名`, `sheng_name`, `SHENG_MC`

### city_code
`市代码`, `市代码_`, `CITY_CODE`, `shi`, `DSDM`, `SJXZQDM`, `citycode`, `地市码`, `市代码_1`, `adcode`, `DQDM`, `SHI`

### city_name
`市级`, `市名`, `市名_1`, `CITY_NAME`, `shi_name`, `DSName`, `SJXZQMC`, `地市名`, `地市级`, `adname`, `cityname`, `市名称`, `市区名`, `DSJGZQYMC`, `DQMC`, `SHI_MC`

### county_code
`区县码`, `COUNTY_COD`, `xian`, `QXDM`, `XJXZQDM`, `县代码`, `县代码_`, `县区代`, `县区代_`, `DistID`, `DistID_1`, `QXJGZQYMC`, `DISTRICTID`

### county_name
`区县级`, `区县名`, `COUNTY_NAM`, `xian_name`, `QXMC`, `XJXZQMC`, `县名`, `县名称`, `县区名`, `县区名_`, `DistName`, `DistName_1`, `XIAN_MC`, `XIAN`, `县区码`

### township_code
`乡镇码`, `TOWN_CODE`, `xiang`, `乡代码`, `XZXZQDM`, `乡镇代`, `乡镇_12`, `StreetID`, `StreetCODE`, `STREET_ID`, `STREET_COD`, `XIANG`, `XZJDM`, `镇代码_`, `街道码`

### township_name
`乡镇级`, `乡镇名`, `乡镇名_`, `TOWN_NAME`, `xiang_name`, `XZXZQMC`, `乡名称`, `StreetName`, `StreetNa_1`, `XIANG_MC`, `XZJMC`, `SJGZQYMC`, `XZJGZQYMC`

### village_code
`XZQDM`, `xzqdm`, `AREA_CODE`, `PAC`, `code`, `CODE`, `村代码`, `村级码`, `CJDCQDM`, `zldwdm`, `area_code`, `sqbm`, `SQBM`, `CUNDM`, `BSM`, `comid`, `comid_1`, `BLOCK_CODE`, `BLOCK_CO_1`, `BLOCK_ID`, `CSDI_ADMIN`, `AREA_ID`, `CACODE`, `DJZQDM`, `XJDM`, `XJDM1`, `CZCUNDM`, `SQCDM`, `XZBM`, `pcode`, `CUN`

### village_name
`XZQMC`, `xzqmc`, `NAME`, `name`, `Name`, `村名称`, `村级名`, `CJDCQMC`, `zldwmc`, `area_name`, `sqmc`, `CUNMC`, `村名`, `comname`, `comname_1`, `BLOCK_NAME`, `NAME_TC`, `NAME_EN`, `CNAME`, `ENAME`, `PNAME`, `SNAME`, `DJZQMC`, `XJMC`, `XJMC1`, `CZCUNMC`, `SQCMC`, `行政村`, `cun_name`, `CJGZQYMC`, `村级`, `CUN_MC`, `cun`, `XZQM`

### note
`BZ`, `备注`, `Note_`, `HDMC`, `desc`

### hk_district_name
`DISTRICT_T`, `DISTRICT_E`, `DISTRICT_C`

### hk_subunit
`PPU`, `SPU`, `TPU`, `Subunit`

### hk_new_town
`NewTown_en`, `NewTown_Tc`, `NewTown_Sc`

### macau_zone
`ZONA`

### forestry_bureau
`LIN_YE_JU`, `LIN_YE_JU_`, `lin_ye_ju`, `LYJ_NAME`, `管局名`, `MS`

### forestry_farm
`LIN_CHANG`, `LIN_CHANG_`, `LC_NAME`

### community_category
`类别`, `类型`

### community_note
`特注`, `名称`, `编码`, `区代码`, `版本号`

### admin_level
`area_level`, `area_lev_1`

## 系统字段（不参与映射）

以下字段为 GIS 系统内部字段或计算字段，不参与统一映射：

- `OBJECTID`, `FID`, `OID_`, `ID` — 内部唯一标识
- `Shape_Length`, `Shape_Area`, `SHAPE_Leng`, `SHAPE_Area` — 几何计算字段
- `x`, `y`, `X`, `Y`, `坐标x`, `坐标y`, `x中心点`, `y中心点` — 坐标字段
- `xmin`, `ymin`, `xmax`, `ymax` — 边界框
- `YSDM`, `MSSM` — 要素代码/描述码
- `KZMJ`, `JSMJ`, `DCMJ`, `MJ`, `TDMJ`, `ComSqua` — 面积字段
- `BORNTIME`, `ENTIID`, `ELEMID`, `FROMENTIID`, `SOURCE` — 元数据字段
- `GlobalID`, `gml_id`, `GID`, `TEMPID`, `XH` — 全局标识
- `gridcode`, `OID_`, `id` — 内部索引
- `area_type`, `AREA_TYPE` — 区域类型标识
- `nd`, `xzq_lx`, `xzq_jb`, `xzq_sy`, `canton_ext` — 属性标识
- `_hex_*` — DBF 11字节限制导致的截断字段名
- `Layer`, `Code`, `level` — 辅助元数据
- 澳门人口统计字段: `POPULATION`, `DENSITY`, `FLAT_SUM`, `FLAT_EMP`, `FLAT_OCC`, `FAMILY`, `ELDERLY`, `ELDERLY_RA`, `BEGIN_LIFE`, `END_LIFESP`, `DATA_OWNER`, `webmap.WMC`

## 已知不可映射字段

上海村界（2上海村社区界-第二套）中存在 **UTF-8 中文字段名被 DBF 11 字节限制截断** 的情况：

- `.cpg` 文件声明 UTF-8，字段名实际也是 UTF-8 编码
- DBF 字段名 11 字节限制导致 UTF-8 三字节中文字符被截断在中间
- 截断后的字节序列是合法的 UTF-8 前缀，不是 GBK 乱码
- 涉及字段：所属街道、居委会、功能区、网格、责任网格、原居委会、旧居委会、村居类别等
- 通过截断模式分析和数据值验证，完整字段名已恢复（见 CHANGELOG.md）
- 这些字段的管理信息已由其他可映射字段覆盖（`StreetID` → `township_code`，`BLOCK_ID` → `village_code` 等）

## Dry Run 验证结果

- 总数据集：58 个
- 完全映射：52 个（90%）
- 部分映射（含不可恢复的乱码字段）：2 个（上海2套）
- 管理层级字段覆盖率：**100%**（所有省份的省/市/县/乡/村层级字段均可映射）
- 港澳特殊字段覆盖率：100%
- 林业局/林场字段覆盖率：100%

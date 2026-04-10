# MCP Query Results: First 5 Nodes

## Query Details
- **Date**: 2026-04-10
- **Entity**: Node
- **Limit**: 5 records
- **Order**: By Id (ascending)

## MCP Server Status
✓ **Connection**: Successfully connected and authenticated
✓ **OAuth Token**: Valid
✓ **S2C Token**: Available and auto-refreshed

## Query Results

Retrieved **5 Node records** from the Infrastructure domain:

### 1. Node ID: 17694
- **Name**: DEMUC0001.SDH001
- **Location**: Germany, Munich (site-based naming convention)
- **Network Address**: (empty)
- **Serial Number**: (empty)
- **Status**: InService (InventoryStatusId: 3)
- **Site ID**: 139524
- **Equipment Definition ID**: 2841
- **In-Service Date**: 2011-06-09 17:56:52

### 2. Node ID: 17695
- **Name**: GBLON0001.SDH001
- **Location**: United Kingdom, London (site-based naming convention)
- **Network Address**: A-444-5-296-211
- **Serial Number**: 65543331118
- **Status**: InService (InventoryStatusId: 3)
- **Site ID**: 139522
- **Equipment Definition ID**: 2841
- **In-Service Date**: 2011-06-09 18:07:07

### 3. Node ID: 17696
- **Name**: IEDUB0001.SDH001
- **Location**: Ireland, Dublin (site-based naming convention)
- **Network Address**: (empty)
- **Serial Number**: (empty)
- **Status**: InService (InventoryStatusId: 3)
- **Site ID**: 139523
- **Equipment Definition ID**: 2841
- **In-Service Date**: 2011-06-09 18:06:32

### 4. Node ID: 17697
- **Name**: NLAMS0001.SDH001
- **Location**: Netherlands, Amsterdam (site-based naming convention)
- **Network Address**: (empty)
- **Serial Number**: (empty)
- **Status**: InService (InventoryStatusId: 3)
- **Site ID**: 139521
- **Equipment Definition ID**: 2841
- **In-Service Date**: 2011-06-09 19:21:35

### 5. Node ID: 17698
- **Name**: IEDUB0001.SDH002
- **Location**: Ireland, Dublin (site-based naming convention)
- **Network Address**: (empty)
- **Serial Number**: (empty)
- **Status**: InService (InventoryStatusId: 3)
- **Site ID**: 139523
- **Equipment Definition ID**: 2850
- **In-Service Date**: 2011-06-10 09:34:05

## Key Observations

1. **Geographic Distribution**: The first 5 nodes span multiple European locations:
   - Germany (Munich)
   - United Kingdom (London)
   - Ireland (Dublin - 2 nodes)
   - Netherlands (Amsterdam)

2. **Naming Convention**: All nodes follow a pattern: `[CountryCode][City][Sequence].[Technology][Sequence]`
   - Example: `GBLON0001.SDH001` = GB (Great Britain) + LON (London) + 0001 + SDH + 001

3. **Technology**: All nodes are SDH (Synchronous Digital Hierarchy) equipment

4. **Status**: All 5 nodes are currently "InService" (status ID: 3)

5. **Timeline**: All nodes were commissioned within a 24-hour period in June 2011

6. **Equipment Definitions**:
   - 4 nodes use Equipment Definition 2841
   - 1 node uses Equipment Definition 2850

7. **Data Completeness**:
   - Only 1 out of 5 nodes has Network Address and Serial Number populated
   - Node GBLON0001.SDH001 has complete data

## Technical Details

### Query Syntax Used
```
Entity: Node
Columns: Id, Name, NetworkAddress, SerialNumber, InventoryStatusId, SiteId, EquipmentDefinitionId, InServiceDate
Filter: (none)
OrderBy: Id
Limit: 5
```

### Entity Schema Summary
The Node entity (in Infrastructure domain) contains:
- 57 total properties
- Key identifiers: Id, Name (unique), SerialNumber
- Network data: NetworkAddress, NetworkRole, Configuration
- Location data: SiteId, RackId, RackFrameId, MapX, MapY
- Equipment data: EquipmentDefinitionId, HardwareRevision, SoftwareVersion
- Status tracking: InventoryStatusId, InServiceDate, OutOfServiceDate
- Power & capacity: AcPowerConsumption, DcPowerConsumption, HeatEmission

## Conclusion

The MCP query was successful. The server is fully operational and able to retrieve network equipment data from the Infrastructure domain. The query returned detailed information about 5 SDH nodes deployed across European locations, demonstrating the system's capability to track network equipment with comprehensive metadata including location, status, and service dates.

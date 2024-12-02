## Task Description
You are a POD information service AI assistant. Your task is to organize the POD information into .json format. I will attach PODs pdf and your goal is to extract the information I need. The needed information is as following: 

1. **Delivery Number (DN/SO)**
The first few codes of DN/SO are the same and will be separated by "/", for example: 11240074345/4347/4349. DN/SO should be intercepted one by one and if there is more than one DN/SO, representing all by array. 

1. **Shipper**

2. **Consignee**

3. **Ship to Address**

4. **Pallet Quantity** 
   - Can be found in "Pallets" or "Anzahl der Paktstücke"

5. **POD Date**
   - Date in the file or "Ausgefertigt"
   - Format as dd-mm-yyyy

6. **Shipping Signed Status**
   - Check if signed in "Unterschrift und Stempel des Empfängers" cell

7. **Other Valuable Information**
such as weight, transport code and so on

Below is a sample extracted POD information organized as markdown table, and the result I would like to output:

example 1: 

| Cell Number | Field Name | Translation (English) | Content (Extracted Information) |
|------------|------------|----------------------|--------------------------------|
| 1 | Absender | Shipper | ASUS EUROPE B.V., PAASHEUVELWEG 25, 1105 BP AMSTERDAM NH, NETHERLANDS |
| 2 | Empfänger | Consignee | CPCDI, RUA MONTE DOS PIPOS NO 649, 4460-059 GUIFOES, PORTUGAL |
| 3 | Auslieferungsort des Gutes (Ort, Land) | Delivery Location (City, Country) | 4460-059 GUIFOES, PORTUGAL |
| 4 | Ort und Tag der Übernahme des Gutes (Ort, Land, Datum) | Place and Date of Goods Acceptance (City, Country, Date) | WALKER, 6222 NE MAASTRICHT, 08-Aug-24 |
| 5 | Beigefügte Dokumente | Attached Documents | Not explicitly provided |
| 6 | Kennzeichen und Nummern | Identification and Numbers | 16240017204 |
| 7 | Anzahl der Paktstücke | Number of Packages | 1 |
| 8 | Art der Verpackung | Type of Packaging | Pallet |
| 9 | Bezeichnung des Gutes | Description of Goods | Not explicitly provided |
| 10 | Statistiknummer | Statistical Number | Not explicitly provided |
| 11 | Bruttogewicht in kg | Gross Weight (kg) | 221.00 |
| 12 | Umfang in m³ | Volume (m³) | Not explicitly provided |
| 13 | Anweisungen des Absenders | Instructions from Shipper | Delivery date: 12-08, ASUS Shipment: PTB20240809-01 |
| 14 | Frachtzahlungsanweisungen | Freight Payment Instructions | Not explicitly provided |
| 15 | Rückerstattung | Reimbursement | Not explicitly provided |
| 16 | Frachtführer (Name, Anschrift, Land) | Carrier (Name, Address, Country) | SERVIROAD EUROPE BY 23, HAZELDONK 6253, NETHERLANDS |
| 17 | Nachfolgende Frachtführer (Name, Anschrift, Land) | Subsequent Carriers (Name, Address, Country) | Not explicitly provided |
| 18 | Vorbehalte und Bemerkungen des Frachtführer | Carrier's Reservations and Remarks | Not explicitly provided |
| 19 | Besondere Vereinbarungen | Special Agreements | Not explicitly provided |
| 20 | Ladeadresse Ankunftszeit, Abfahrtzeit, Gesamtzeit / Entladeadresse Ankunftszeit, Abfahrtzeit, Gesamtzeit | Loading Address Arrival Time, Departure Time, Total Time / Unloading Address Arrival Time, Departure Time, Total Time | Not explicitly provided |
| 21 | Ausgefertigt in am | Issued in, on | 08-August-2024 |
| 22 | Unterschrift und Stempel des Absenders | Signature and Stamp of Shipper | KRISTEL PAULINA WALKER INTERNATIONAL |
| 23 | Unterschrift und Stempel des Frachtführers | Signature and Stamp of Carrier | SERVIROAD EUROPE BY 23, HAZELDONK 6253, NETHERLANDS |
| 24 | Unterschrift und Stempel des Empfängers | Signature and Stamp of Consignee | CPCDI, RUA MONTE DOS PIPOS NO 649, 4460-059 GUIFOES, PORTUGAL |
| 25 | Code Frachtführer Nr | Carrier Code | NL S00194864 |

Output
```json
{
    "Delivery Number (DN/SO)": ["16240017204"],
    "Shipper": "ASUS EUROPE B.V., PAASHEUVELWEG 25, 1105 BP AMSTERDAM NH, NETHERLANDS",
    "Consignee": "CPCDI, RUA MONTE DOS PIPOS NO 649, 4460-059 GUIFOES, PORTUGAL",
    "Ship to Address": "WALKER, 6222 NE MAASTRICHT",
    "Pallet Quantity": "1",
    "POD Date": "08-08-2024",
    "Signed": "Yes"
}
```

## Important Requirements
Here are a few points that MUST keep in mind: 
1. The markdown table order I provided corresponds with the POD pdf cells.
2. You must include all keys I provided in the example output, but you can add any other valuable information in POD.
3. Give me all information in one .json file

The PODs for the task are attached
You MUST output in the format I specified!!

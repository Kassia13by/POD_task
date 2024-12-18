## Prompt
Imagine you are a meticulous document analyst tasked with extracting structured data from transport documentation in a way that preserves accuracy and ensures clarity. Your primary task is to organize the POD information into ```.json``` format. I will attach PODs pdf and your goal is to extract the information I need. The needed information is as following.

Let's systematically approach the data extraction process.

First, scan the document for the Delivery Number (DN/SO), ensuring each component of the number is correctly parsed.
1. **Delivery Number (DN/SO)**
   - The first few codes of DN/SO are the same and will be separated by "/", for example: 11240074345/4347/4349. DN/SO       should be intercepted one by one and if there is more than one DN/SO, representing all by array. 

Next, focus on identifying and categorizing key fields such as
2. **Shipper**
3. **Consignee**
4. **Ship to Address**

Finally, confirm if all required details, including the 
5. **Pallet Quantity** 
   - Can be found in "Pallets" or "Anzahl der Paktstücke"
6. **POD Date**
   - Date in the file or "Ausgefertigt"
   - Consider scenarios where some fields are ambiguously written. For instance, convert POD date to dd-mm-yyyy
7. **Shipping Signed Status**
   - Check if signed in "Unterschrift und Stempel des Empfängers" cell
   - If the signature field is unmarked, set the value as No
8. **Other Valuable Information**
   - Think of this task like assembling a puzzle. Each piece of information may be critical to creating a complete
     picture. For instance, information such as weight, transport code and so on could be important addtional
     information.

Below is a sample extracted POD information organized as markdown table, and the result I would like you to output:

example: 

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

Using the structured approach outlined above, systematically extract and format the data. Here are a few points that MUST keep in mind: 
1. The markdown table order I provided corresponds with the POD pdf cells.
2. You must include all keys I provided in the example output, but you can add any other valuable information in POD.
3. Give me all information in one ```.json``` file

The PODs for the task are attached
The process of extracting data from PODs is akin to organizing ingredients for a recipe. Each detail contributes to the final dish: a clean, organized ```.json``` file. Thus, you MUST output in the format I specified!!

----

## Prompt 設計說明

主要採用「思維故事 (Story of Thought, SoT)」方法設計，即將敘事視為設計的核心原則，結合邏輯與創造力，建立引導明確的對話架構。SoT 包含三個部分：問題闡明 (Question Clarification)、敘事生成 (Narrative Generation)、問題求解 (Problem Solving)。以下詳述並以設計的 prompt 為例說明

1. 問題闡明 (Question Clarification)：將複雜問題拆解為多個子問題，並透過角色扮演引導 AI 理解情境。例如，將 AI 設定為「文件分析專家」或「資料結構化助理」，幫助其專注於具體任務需求，避免模糊與歧義。
   Prompt:
   ```Imagine you are a meticulous document analyst tasked with extracting structured data from transport documentation in a way that preserves accuracy and ensures clarity. Your primary task is to organize the POD information into .json format. I will attach PODs pdf and your goal is to extract the information I need. The needed information is as following.```
2. 敘事生成 (Narrative Generation)：可透過五種敘事技術，幫助 AI 在訊息處理中構建邏輯（不一定要全部包含）：
   - 逐步披露 (Progressive Disclosure)：分階段揭示問題脈絡，使 AI 的思考過程循序漸進。
     Prompt: ```Let's systematically approach the data extraction process.......```
   - 分支敘述 (Branching)：從不同角度探索可能性，提升問題求解的全面性。
     Prompt: ```Date in the file or "Ausgefertigt" Consider scenarios where some fields are ambiguously written. For instance, convert POD date to dd-mm-yyyy```(逐步披露列點底下的小點說明)
   - 類比 (Analogy)：用熟悉的情境解釋複雜概念。
     Prompt: ```Think of this task like assembling a puzzle......```
   - 類比推理 (Analogical Reasoning)：以相似性聯繫不同概念，建構邏輯推理基礎。
   - 隱喻 (Metaphor)：以比喻方式描述問題核心。
     Prompt: ```The process of extracting data from PODs is akin to organizing ingredients for a recipe. Each detail contributes to the final dish: a clean, organized .json file.```
3. 問題求解 (Problem Solving)：整合敘事，得出結論。
   Prompt: ```Using the structured approach outlined above, systematically extract and format the data......```

此外，亦採用少樣本學習（Few-Shot Learning）穿插其中，提升模型的準確性。例如 markdown table 描述 pdf 檔案內容架構以及範例的 ```.json``` 輸出。

[參考資料](https://www.researchgate.net/publication/385292073_Can_Stories_Help_LLMs_Reason_Curating_Information_Space_Through_Narrative)







# POD_task

A task for extracting and organizing Proof of Delivery (POD) information into structured JSON format using Claude 3.5 Sonnet (October 2024 version).

## Repository Contents

- `pod_data.json`: Extracted POD information in JSON format
- `pod_prompt.md`: Prompt template and instructions for Claude

## Features

- Extracts key POD information including:
 - Delivery Numbers (DN/SO)
 - Shipper details
 - Consignee information
 - Shipping addresses
 - Pallet quantities
 - POD dates (formatted as dd-mm-yyyy)
 - Signature status
 - Additional metadata (weights, transport codes, etc.)

- Handles multiple delivery numbers with proper array formatting
- Maintains consistent date formatting
- Preserves important shipping metadata

## Example Output Structure

```json
{
   "doc1": {
    "Delivery Number (DN/SO)": ["16240013881/0500901"],
    "Shipper": "ASNL (ASUS Europe B.V.) c/o Geodis, Tasmanweg 14, 5928 LH VENLO, THE NETHERLANDS",
    "Consignee": "CPCDI-COMPANHIA PORTUGUESA DE COMPUTADORES DISTRIBUICAO, RUA MONTE DOS PIPOS 649, GUIFOES, 4460-059, Portugal",
    "Ship to Address": "5928 LH Venlo, Netherlands",
    "Pallet Quantity": "1",
    "POD Date": "04-07-2024",
    "Signed": "Yes",
    "Additional Info": {
      "Shipment": "1311154",
      "Pallet Type": "BLOCK (100 CM x 120 CM)",
      "Cartons": "7",
      "Volume": "0,315",
      "Weight": "40,900",
      "Net Weight": "25,900"
    }
}

## Introduction

The **SuiteTalk Connector** is a robust integration tool that empowers developers to seamlessly connect and interact with the NetSuite ERP (Enterprise Resource Planning) system using web services. By leveraging the power of SuiteTalk API, the SuiteTalk Connector enables the automation of business processes, data synchronization, and the creation of custom integrations with NetSuite.

The SuiteTalk Connector acts as a bridge between your application and NetSuite, simplifying the integration process and abstracting the complexities of interacting with the underlying SuiteTalk API. It provides a higher-level interface, allowing developers to focus on business logic rather than low-level API implementation details.

### Key Features

The SuiteTalk Connector offers the following key features:

1. **Authentication**: The connector handles secure authentication with NetSuite, ensuring authorized access to the API using the appropriate credentials.

2. **API Interaction**: It provides a simplified interface for making API requests to NetSuite, abstracting the underlying SOAP (Simple Object Access Protocol) communication and facilitating seamless integration with your application.

3. **Data Mapping**: The connector simplifies the mapping and transformation of data between your application and NetSuite's data model, ensuring smooth data synchronization and integration.

4. **Error Handling**: It includes comprehensive error handling mechanisms, allowing for robust error management and graceful recovery during API interactions.

5. **Performance Optimization**: The connector incorporates optimizations to enhance performance, such as request batching, minimizing network round trips, and optimizing data retrieval and update operations.

6. **Flexibility**: The SuiteTalk Connector is highly customizable and can be extended to accommodate specific integration requirements. It enables developers to build tailored solutions that align with their unique business processes.

### Benefits of Using SuiteTalk Connector

- **Streamlined Integration**: The connector simplifies the integration process, enabling efficient communication between your application and NetSuite.

- **Customizability**: Developers can extend and customize the connector to meet specific integration needs and business requirements.

- **Automation and Efficiency**: The integration capabilities offered by the connector automate business processes, improving efficiency and reducing manual effort.

- **Real-Time Data Sync**: Achieve real-time data synchronization between your application and NetSuite, ensuring accurate and up-to-date information.

By leveraging the SuiteTalk Connector, developers can unlock the full potential of NetSuite's API, enabling seamless integration, customization, and automation of business processes. Experience streamlined integration and harness the power of NetSuite with the SuiteTalk Connector.

## Installation

To install the SuiteTalk Connector using pip and Git, run the following command:

```shell
$ python -m pip install 'git+ssh://git@github.com/ideabosque/suitetalk_connector.git@main#egg=suitetalk_connector'
```

## Configuration

To configure the NetSuite SuiteTalk Connector, you'll need to set up the following files and environment variables:

### .env File

Create a `.env` file in the project directory with the following example configuration:

```plaintext
ACCOUNT=*******
CONSUMER_KEY=****************************************************************
CONSUMER_SECRET==****************************************************************
TOKEN_ID==****************************************************************
TOKEN_SECRET==****************************************************************
```

Replace the `*******` and `****************************************************************` placeholders with your actual NetSuite account ID, consumer key, consumer secret, token ID, and token secret.

### netsuitemappings_soap.json File

Create a `netsuitemappings_soap.json` file in the project directory with the appropriate mappings for the desired transaction types, attributes, and data types. Here is an example configuration:

```json
{
  "transaction_attributes": [
    "entity",
    "email",
    "salesRep",
    "subsidiary",
    "customForm",
    "class",
    "location",
    "billingAddress",
    "shippingAddress",
    "pnRefNum",
    "otherRefNum",
    "source",
    "memo",
    "message",
    "shipDate",
    "shippingCost",
    "terms",
    "paymentMethod",
    "shipMethod",
    "itemList",
    "shipDate",
    "tranDate",
    "orderStatus",
    "customFieldList",
    "status",
    "createdFrom"
  ],
  "transaction_data_type": {
    "salesOrder": "ns19:SalesOrder",
    "opportunity": "ns19:Opportunity",
    "estimate": "ns19:Estimate",
    "returnAuthorization": "ns23:ReturnAuthorization"
  },
  "transaction_item_data_type": {
    "salesOrder": "ns19:SalesOrderItem",
    "opportunity": "ns19:OpportunityItem",
    "estimate": "ns19:EstimateItem",
    "returnAuthorization": "ns23:ReturnAuthorizationItem"
  },
  "transaction_item_list_data_type": {
    "salesOrder": "ns19:SalesOrderItemList",
    "opportunity": "ns19:OpportunityItemList",
    "estimate": "ns19:EstimateItemList",
    "returnAuthorization": "ns23:ReturnAuthorizationItemList"
  },
  "person_data_type": {
    "customer": "ns13:Customer",
    "contact": "ns13:Contact"
  },
  "person_addressbook_list_data_type": {
    "customer": "ns13:CustomerAddressbookList"
  },
  "person_addressbook_data_type": {
    "customer": "ns13:CustomerAddressbook"
  },
  "item_data_type": {
    "inventoryItem": "ns17:InventoryItem",
    "nonInventoryResaleItem": "ns17:NonInventoryResaleItem",
    "lotNumberedInventoryItem": "ns17:LotNumberedInventoryItem"
  },
  "lookup_join_fields": {
    "itemFulfillment": {
      "base": [
        "@|custbody_bol_id",
        "@|custbody_bol_number",
        "fulfill_last_modified_date|lastModifiedDate",
        "fulfill_internal_id|internalId",
        "fulfill_ship_status|shipStatus"
      ],
      "lines": [
        "serial_numbers|serialNumbers"
      ],
      "created_from_types": [
        "salesOrder"
      ]
    },
    "invoice": {
      "base": [
        "invoice_tran_id|tranId",
        "invoice_status|status",
        "invoice_tran_date|tranDate",
        "invoice_total|total"
      ],
      "lines": [],
      "created_from_types": [
        "salesOrder"
      ]
    },
    "vendorBill": {
      "base": [
        "transaction_number|transactionNumber",
        "due_date|dueDate",
        "erp_bill_ref|internalId"
      ],
      "lines": [],
      "created_from_types": [
        "purchaseOrder"
      ]
    },
    "itemReceipt": {
      "base": [
        "receipt_internal_id|internalId",
        "receipt_created_date|createdDate"
      ],
      "lines": [],
      "created_from_types": [
        "purchaseOrder"
      ]
    },
    "returnAuthorization": {
      "created_from_lookup_type": "salesOrder"
    }
  },
  "lookup_record_fields": {
    "salesOrder": {
      "field": "custbody_pct_so_ecomso",
      "search_data_type": "ns5:TransactionSearchBasic"
    },
    "opportunity": {
      "field": "custbody_bid_reference",
      "search_data_type": "ns5:TransactionSearchBasic"
    },
    "estimate": {
      "field": "otherRefNum",
      "search_data_type": "ns5:TransactionSearchBasic"
    },
    "returnAuthorization": {
      "field": "custbody_rma_reference",
      "search_data_type": "ns5:TransactionSearchBasic"
    },
    "inventoryItem": {
      "field": "itemId",
      "search_data_type": "ns5:ItemSearchBasic"
    },
    "lotNumberedInventoryItem": {
      "field": "itemId",
      "search_data_type": "ns5:ItemSearchBasic"
    },
    "customer": {
      "field": "entityId",
      "search_data_type": "ns5:CustomerSearchBasic"
    },
    "contact": {
      "field": "entityId",
      "search_data_type": "ns5:ContactSearchBasic"
    },
    "vendor": {
      "field": "entityId",
      "search_data_type": "ns5:VendorSearchBasic"
    },
    "subsidiary": {
      "field": "name",
      "search_data_type": "ns5:SubsidiarySearchBasic"
    },
    "location": {
      "field": "name",
      "search_data_type": "ns5:LocationSearchBasic"
    },
    "classification": {
      "field": "name",
      "search_data_type": "ns5:ClassificationSearchBasic"
    },
    "employee": {
      "field": "entityId",
      "search_data_type": "ns5:EmployeeSearchBasic"
    },
    "priceLevel": {
      "field": "name",
      "search_data_type": "ns5:PriceLevelSearchBasic"
    },
    "inventoryNumber": {
      "field": "inventoryNumber",
      "search_data_type": "ns5:InventoryNumberSearchBasic"
    }
  },
  "lookup_select_values": {
    "terms": {
      "values": {
        "Net 10": "1",
        "Net 15": "2",
        "Net 20": "3"
      }
    },
    "paymentMethod": {
      "values": {
        "ACH": "1",
        "American Express": "2",
        "Cash": "3",
        "Check": "4",
        "Discover": "5",
        "Master Card": "6",
        "VISA": "7",
        "Wire": "8"
      }
    },
    "taxSchedule": {},
    "customForm": {},
    "shipMethod": {
      "values": {
        "Truck": "1",
        "UPS": "2",
        "UPS 2nd Day Air®": "3",
        "UPS Next Day Air®": "4",
        "UPS Next Day Air® Early A.M.®": "5",
        "UPS® Ground": "6"
      },
      "record_type": "shipItem",
      "field": "displayName"
    },
    "salesRep": {
      "record_type": "employee",
      "field": "entityId"
    },
    "class": {
      "record_type": "classification",
      "field": "name"
    },
    "subsidiary": {
      "record_type": "subsidiary",
      "field": "name"
    },
    "location": {
      "record_type": "location",
      "field": "name"
    },
    "custbody_delivery_option": {
      "values": {
        "Standard": "4",
        "Premium": "5",
        "Expedited": "6"
      }
    },
    "custentityyyy": {
      "record_type": "customlist_yyyy_list",
      "field": "name"
    },
    "custentity_program_sales_rep": {
      "record_type": "employee",
      "field": "entityId"
    },
    "custentityxxx": {
      "record_type": "customlistxxx",
      "field": "name"
    }
  },
  "custom_records": {
    "customrecord_shipping_carrier": "111"
  },
  "item_detail_record_types": [
    "purchaseOrder",
    "returnAuthorization"
  ],
  "inventory_detail_record_types": [
    "purchaseOrder",
    "itemReceipt",
    "itemFulfillment",
    "salesOrder",
    "returnAuthorization"
  ],
  "transaction_update_statuses": {
    "salesOrder": ["Cancelled"],
    "returnAuthorization": []
  }
}
```

**Parameters:**
- `transaction_attributes`: This parameter specifies the list of attributes that will be used for any transaction in the NetSuite system.
- `transaction_data_type`: This parameter defines the SOAP data type associated with each transaction type in NetSuite. It specifies the data type used to represent the transaction data.
- `transaction_item_data_type`: This parameter determines the SOAP data type associated with the items within a transaction. It indicates the data type used to represent individual items in a transaction.
- `transaction_item_list_data_type`: This parameter indicates the SOAP data type for the list of items within a transaction. It specifies the data type used to represent the collection of items in a transaction.
- `person_data_type`: This parameter defines the SOAP data type for person-related records, such as customers and contacts, in NetSuite.
- `person_addressbook_data_type`: This parameter specifies the SOAP data type for the address book of a person, typically used for customers or contacts in NetSuite.
- `person_addressbook_list_data_type`: This parameter indicates the SOAP data type for the list of address books associated with a person, usually used for customers or contacts in NetSuite.
- `item_data_type`: This parameter determines the SOAP data type for various item types in NetSuite, such as inventory items, non-inventory resale items, and lot-numbered inventory items.
- `lookup_join_fields`: This parameter includes configurations for joining related records in NetSuite. It defines how different records are linked together in search results.
- `lookup_record_fields`: This parameter contains configurations for field mappings when looking up records in NetSuite. It specifies the fields used for searching and linking records.
- `lookup_select_values`: This parameter provides configurations for select field values in NetSuite. It defines the possible values and their corresponding internal IDs for specific fields.
- `custom_records`: This parameter contains configurations for custom records in NetSuite. It specifies the internal IDs of custom records that can be used in the integration.
- `item_detail_record_types`: This parameter lists the record types in NetSuite that have detailed information about items. For example, purchase orders and return authorizations may have additional item details.
- `inventory_detail_record_types`: This parameter lists the record types in NetSuite that have detailed information about inventory-related transactions, such as purchase orders, item receipts, item fulfillments, sales orders, and return authorizations.
- `transaction_update_statuses`: This parameter serves two pivotal purposes for updating records. Firstly, it facilitates updates only when the transaction status aligns with the statuses listed. Secondly, it ensures updates occur if the transaction's record type is absent from the keys within `transaction_update_statuses`.

### Sample Configuration

Here is a sample configuration file that loads the environment variables and sets up the NetSuite SuiteTalk Connector:

```python
import logging
import os
import sys
import json
from dotenv import load_dotenv
from suitetalk_connector import SOAPConnector

logging.basicConfig(stream=sys.stdout, level=logging.INFO)
logger = logging.getLogger()

load_dotenv()
setting = {
    "ACCOUNT": os.getenv("ACCOUNT"),
    "CONSUMER_KEY": os.getenv("CONSUMER_KEY"),
    "CONSUMER_SECRET": os.getenv("CONSUMER_SECRET"),
    "TOKEN_ID": os.getenv("TOKEN_ID"),
    "TOKEN_SECRET": os.getenv("TOKEN_SECRET"),
    "VERSION": "2021_2_0",
    "TIMEZONE": "America/Los_Angeles",
    "NETSUITEMAPPINGS": json.load(
        open(
            f"{os.path.abspath(os.path.dirname(__file__))}/netsuitemappings_soap.json",
            "r",
        )
    )
}

soap_connector = SOAPConnector(logger, **setting)
```

Ensure that you have the required Python packages installed, including `dotenv`. You can install them using the following command:

```shell
$ python -m pip install dotenv
```

Make sure to replace the path to the `netsuitemappings_soap.json` file with the appropriate location in your project directory.

With this configuration, you can now use the `soap_connector` object to interact with the NetSuite SuiteTalk API.

## Usage

To use the NetSuite SuiteTalk Connector, you can follow the examples below:

### Get the ID value of a dropdown custom field for a specific record type

Use the `get_select_value_id` method to retrieve the ID value of a dropdown custom field.

Parameters:
- `value`: The value of the dropdown option.
- `custom field name`: The name of the custom field.
- `record_type`: The record type in which the custom field is defined.

```python
id = soap_connector.get_select_value_id(
    "To Be Determined",
    "custbody_carrier_other",
    record_type="salesOrder"
)
```

This method will return the ID value associated with the specified dropdown option.

### Get a record by its internal ID

Use the `get_record` method to retrieve a record by its internal ID.

Parameters:
- `record_type`: The type of the record.
- `internalId`: The internal ID of the record.

```python
record = soap_connector.get_record(
    "purchaseOrder",
    "11234567"
)
```

This method will return the record object corresponding to the specified record type and internal ID.

### Get transactions

Retrieve transactions based on the cut date and other parameters.

Parameters:
- `record_type`: The transaction record type. Choose from the following options:
  - "salesOrder"
  - "invoice"
  - "purchaseOrder"
  - "estimate"
  - "opportunity"
  - "returnAuthorization"
  - "itemFulfillment"
  - "itemReceipt"
  - "vendorCredit"
  - "vendorPayment"
  - "inventoryAdjustment"
  - "creditMemo"
  - "inventoryTransfer"
- `kwargs`: Additional parameters for filtering and customization.

```python
kwargs = {
    "cut_date": "2022-02-04T16:00:00+00:00",
    "limit": 100,
    "hours": 0.25,
    "inventory_detail": True,
    "subsidiary": "ABC",
}

transactions = soap_connector.get_transactions(
    "itemReceipt", **kwargs
)
```

This method will retrieve transactions of the specified record type based on the provided parameters.

### Get items

Retrieve items based on the cut date and other parameters.

Parameters:
- `record_type`: The item record type. Choose from the following options:
  - "product"
  - "inventory"
  - "inventorylot"
  - "pricelevel"
- `kwargs`: Additional parameters for filtering and customization.

```python
kwargs = {
    "cut_date": "2022-02-04T16:00:00+00:00",
    "limit": 100,
    "hours": 1000,
    "subsidiary": "ABC",
    "item_types": [
        "inventoryItem",
        "lotNumberedInventoryItem",
    ],
    "custom_fields": {
        "custitem3": "kg",
    },
}

items = soap_connector.get_items("inventoryLot", **kwargs)
```

This method will retrieve items of the specified record type based on the provided parameters.

### Get persons

Retrieve persons based on the cut date and other parameters.

Parameters:
- `record_type`: The person record type. Choose from the following options:
  - "customer"
  - "vendor"
  - "company"
  - "contact"
- `kwargs`: Additional parameters for filtering and customization.

```python
kwargs = {
    "cut_date": "2022-02-04T16:00:00+00:00",
    "limit": 100,
    "hours": 0.5,
    "subsidiary": "ABC",
}

persons = soap_connector.get_persons("customer", **kwargs)
```

This method will retrieve persons of the specified record type based on the provided parameters.

**Parameters in `kwargs` for `get_transactions`, `get_items`, and `get_persons`:**

- `cut_date`: The last run of the cut date. Format: YYYY-MM-DDTHH:MM:SS.
- `limit`: The limit amount of records to be retrieved.
- `hours`: The period from the cut date in hours.
- `inventory_detail` (for `get_transactions`): A boolean value indicating whether to retrieve the detail of inventory information.
- `subsidiary`: The subsidiary of the company.
- `item_types` (for `get_items`): A list of item record types to be retrieved.
- `custom_fields` (for `get_items`): A dictionary of custom fields and their values to be used as conditions for retrieving data.


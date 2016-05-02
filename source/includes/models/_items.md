# Items
Either attached to a document or a transaction.

## The item object
> Example object

```json
{
  "id": "oc_it_1460568443g3wu6b48fc3e",
  "object": "item",
  "transaction": "oc_txn_14605672518yko2fd30d23",
  "invoice": nil,
  "credit_note": nil,
  "tax_evidence": "oc_tev_1460565379am3be8f5ef71",
  "description": "Entreprise Plan",
  "unit_extratax_amount": 19900,
  "currency": "USD",
  "quantity": 1,
  "extratax_amount": 19900,
  "tax_rate": 22.0,
  "tax_amount": 4378,
  "gross_amount": 24278,
  "item_exchange": {
    "exchange_rate": 0.8864,
    "exchange_date": "2016-04-13T17:27:24.228Z",
    "exchanged_to_currency": "EUR"
  }
}
```

### Attributes
<table>
  <tbody>
    <tr class="first-row">
      <td class="attribute"><strong>id</strong><br/><span class="details">string</span></td>
      <td><p>-</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>object</strong><br/><span class="details">string, value is "<strong>item</strong>"</span></td>
      <td><p>-</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>transaction</strong><br/><span class="details">string</span></td>
      <td><p>ID of the transaction.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>invoice</strong><br/><span class="details">string</span></td>
      <td><p>ID of the invoice.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>credit_note</strong><br/><span class="details">string</span></td>
      <td><p>ID of the credit note.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>tax_evidence</strong><br/><span class="details">string</span></td>
      <td><p>ID of the tax_evidence.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>description</strong><br/><span class="details">string</span></td>
      <td><p>-</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>unit_extratax_amount</strong><br/><span class="details">integer</span></td>
      <td><p>The unit price of the item without tax.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>currency</strong><br/><span class="details">string</span></td>
      <td><p>3-letter <a href="http://www.xe.com/iso4217.php#section2" target="_blank">ISO code for currency</a>.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>quantity</strong><br/><span class="details">integer</span></td>
      <td><p>A positive integer representing the number of instances of the item.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>extratax_amount</strong><br/><span class="details">integer</span></td>
      <td><p>The unit price multiplied by the quantity.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>tax_rate</strong><br/><span class="details">float</span></td>
      <td><p>Tax rate applied to the item.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>tax_amount</strong><br/><span class="details">integer</span></td>
      <td><p>The tax amount based on the tax rate and the extratax amount.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>gross_amount</strong><br/><span class="details">integer</span></td>
      <td><p>The amount all tax included.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>item_exchange</strong><br/><span class="details">hash</span></td>
      <td><p>The exchange information if needed.</p></td>
    </tr>
  </tbody>
</table>


## Create an item

```
# Definition
POST https://api.octobat.com/transactions/{TRANSACTION_ID}/items
POST https://api.octobat.com/invoices/{INVOICE_ID}/items
POST https://api.octobat.com/credit_notes/{CREDIT_NOTE_ID}/items
```

```shell
# Example Request
$ curl https://api.octobat.com/invoices/oc_in_14619363114yke51e2ce5f/items \
   -u oc_test_skey_tkHCYYOUVrYyY5rBFZxNzgtt: \
   -d tax_evidence="oc_tev_1460565379am3be8f5ef71" \
   -d quantity=1 \
   -d currency="USD" \
   -d unit_extratax_amount=19900 \
   -d description="Entreprise Plan"

# Example response
{
  "id": "oc_it_1460568443g3wu6b48fc3e",
  "object": "item",
  "transaction": nil,
  "invoice": "oc_in_14619363114yke51e2ce5f",
  "credit_note": nil,
  "tax_evidence": "oc_tev_1460565379am3be8f5ef71",
  "description": "Entreprise Plan",
  "unit_extratax_amount": 19900,
  "currency": "USD",
  "quantity": 1,
  "extratax_amount": 19900,
  "tax_rate": 22.0,
  "tax_amount": 4378,
  "gross_amount": 24278,
  "item_exchange": {
    "exchange_rate": 0.8864,
    "exchange_date": "2016-04-13T17:27:24.228Z",
    "exchanged_to_currency": "EUR"
  }
}
```

```ruby
# Example request
>> require "octobat"
Octobat.api_key = "oc_test_skey_tkHCYYOUVrYyY5rBFZxNzgtt"

invoice = Octobat::Invoice.find("oc_in_14619363114yke51e2ce5f")
item = invoice.items.new(
  tax_evidence: "oc_tev_1460565379am3be8f5ef71",
  quantity: 1,
  currency: "USD",
  unit_extratax_amount: 19900,
  description: "Entreprise Plan"
)
item.save

# Example response
#<Octobat::Item id=oc_it_1460568443g3wu6b48fc3e 0x00000a> JSON: {
  "id": "oc_it_1460568443g3wu6b48fc3e",
  "object": "item",
  "transaction": nil,
  "invoice": "oc_in_14619363114yke51e2ce5f",
  "credit_note": nil,
  "tax_evidence": "oc_tev_1460565379am3be8f5ef71",
  "description": "Entreprise Plan",
  "unit_extratax_amount": 19900,
  "currency": "USD",
  "quantity": 1,
  "extratax_amount": 19900,
  "tax_rate": 22.0,
  "tax_amount": 4378,
  "gross_amount": 24278,
  "item_exchange": {
    "exchange_rate": 0.8864,
    "exchange_date": "2016-04-13T17:27:24.228Z",
    "exchanged_to_currency": "EUR"
  }
}
```

### Arguments
<table>
  <tbody>
    <tr class="first-row">
      <td class="attribute"><strong>unit_extratax_amount</strong><br/><span class="badge-warning">required</span></td>
      <td><p>The unit price of the item without tax.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>currency</strong><br/><span class="badge-warning">required</span></td>
      <td><p>3-letter <a href="http://www.xe.com/iso4217.php#section2" target="_blank">ISO code for currency</a>.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>transaction</strong><br/><span class="details">optional, either <strong>transaction</strong> or <strong>invoice</strong> or <strong>credit_note</strong> is required</span></td>
      <td><p>The ID of an existing transaction.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>invoice</strong><br/><span class="details">optional, either <strong>invoice</strong> or <strong>transaction</strong> or <strong>credit_note</strong> is required</span></td>
      <td><p>The ID of an existing invoice.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>credit_note</strong><br/><span class="details">optional, either <strong>credit_note</strong> or <strong>transaction</strong> or <strong>invoice</strong> is required</span></td>
      <td><p>The ID of an existing credit note.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>tax_evidence</strong><br/><span class="details">optional, either <strong>tax_evidence</strong> or <strong>tax_rate</strong> is required</span></td>
      <td><p>The ID of an existing tax evidence. This is where customer and supplier transaction evidences are stored. The tax rate applied to the item is automatically calculated thanks to the evidences.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>tax_rate</strong><br/><span class="details">optional, either <strong>tax_rate</strong> or <strong>tax_evidence</strong> is required</span></td>
      <td><p>The tax rate that you want apply to the item.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>quantity</strong><br/><span class="details">optional, default is 1</span></td>
      <td><p>A positive integer representing the number of instances of the item.</p></td>
    </tr>
    <tr>
      <td class="attribute"><strong>description</strong><br/><span class="details">optional</span></td>
      <td><p>Item's description.</p></td>
    </tr>
  </tbody>
</table>


### Returns
Returns the item object if the creation succeeds. Returns an error if parameters are invalid



## Retrieve an item
```shell
# Definition
GET https://api.octobat.com/invoices/{INVOICE_ID}/items/{ITEM_ID}/
GET https://api.octobat.com/transactions/{TRANSACTION_ID}/items/{ITEM_ID}/
GET https://api.octobat.com/credit_notes/{CREDIT_NOTE_ID}/items/{ITEM_ID}/

# Example Request
$ curl https://api.octobat.com/invoices/oc_in_14619363114yke51e2ce5f/items/oc_it_1461938887kzsf607ad4cf \
   -u oc_test_skey_tkHCYYOUVrYyY5rBFZxNzgtt:

# Example response
{
  "id": "oc_it_1460568443g3wu6b48fc3e",
  "object": "item",
  "transaction": nil,
  "invoice": "oc_in_14619363114yke51e2ce5f",
  "credit_note": nil,
  "tax_evidence": "oc_tev_1460565379am3be8f5ef71",
  "description": "Entreprise Plan",
  "unit_extratax_amount": 19900,
  "currency": "USD",
  "quantity": 1,
  "extratax_amount": 19900,
  "tax_rate": 22.0,
  "tax_amount": 4378,
  "gross_amount": 24278,
  "item_exchange": {
    "exchange_rate": 0.8864,
    "exchange_date": "2016-04-13T17:27:24.228Z",
    "exchanged_to_currency": "EUR"
  }
}
```

```ruby
# Definition
invoice = Octobat::Invoice.find({INVOICE_ID})
invoice.items.find({ITEM_ID})
# or
transaction = Octobat::Transaction.find({TRANSACTION_ID})
transaction.items.find({ITEM_ID})
# or
credit_note = Octobat::CreditNote.find({CREDIT_NOTE_ID})
credit_note.items.find({ITEM_ID})

# Example request
>> require "octobat"
Octobat.api_key = "oc_test_skey_tkHCYYOUVrYyY5rBFZxNzgtt"

invoice = Octobat::Invoice.find("oc_in_14619363114yke51e2ce5f")
invoice.items.find("oc_it_1461938887kzsf607ad4cf")

# Example response
#<Octobat::Item id=oc_it_1460568443g3wu6b48fc3e 0x00000a> JSON: {
  "id": "oc_it_1460568443g3wu6b48fc3e",
  "object": "item",
  "transaction": nil,
  "invoice": "oc_in_14619363114yke51e2ce5f",
  "credit_note": nil,
  "tax_evidence": "oc_tev_1460565379am3be8f5ef71",
  "description": "Entreprise Plan",
  "unit_extratax_amount": 19900,
  "currency": "USD",
  "quantity": 1,
  "extratax_amount": 19900,
  "tax_rate": 22.0,
  "tax_amount": 4378,
  "gross_amount": 24278,
  "item_exchange": {
    "exchange_rate": 0.8864,
    "exchange_date": "2016-04-13T17:27:24.228Z",
    "exchanged_to_currency": "EUR"
  }
}
```


Retrieves the details of an existing item.


### Returns
Returns an item object if a valid identifier was provided.



## List all items

```shell
# Definition
GET https://api.octobat.com/transactions/{TRANSACTION_ID}/items/
GET https://api.octobat.com/invoices/{INVOICE_ID}/items/
GET https://api.octobat.com/credit_notes/{CREDIT_NOTE_ID}/items/

# Example request
$ curl https://api.octobat.com/transactions/oc_txn_1459936947icq9005f4668/items \
   -u oc_test_skey_tkHCYYOUVrYyY5rBFZxNzgtt:

# Example response
{
  "object": "list",
  "has_before": false,
  "has_more": false,
  "total_count": 3,
  "data": [
    {
      "id": "oc_it_1460568443g3wu6b48fc3e",
      "object": "item",
      "transaction": "oc_txn_14605672518yko2fd30d23",
      "invoice": nil,
      "credit_note": nil,
      "tax_evidence": "oc_tev_1460565379am3be8f5ef71",
      "description": "Entreprise Plan",
      "unit_extratax_amount": 19900,
      "currency": "USD",
      "quantity": 1,
      "extratax_amount": 19900,
      "tax_rate": 22.0,
      "tax_amount": 4378,
      "gross_amount": 24278,
      "item_exchange": {
        "exchange_rate": 0.8864,
        "exchange_date": "2016-04-13T17:27:24.228Z",
        "exchanged_to_currency": "EUR"
      }
    },
    {...},
    {...}
  ]
}
```

```ruby
# Definition
transaction = Octobat::Transaction.find({TRANSACTION_ID})
transaction.items.all
# or
invoice = Octobat::Invoice.find({INVOICE_ID})
invoice.items.all
# or
credit_note = Octobat::CreditNote.find({CREDIT_NOTE_ID})
credit_note.items.all

# Example request
>> require "octobat"
Octobat.api_key = "oc_test_skey_tkHCYYOUVrYyY5rBFZxNzgtt"

transaction = Octobat::Transaction.find("oc_txn_14605672518yko2fd30d23")
transaction.items.all

# Example response
#<Octobat::ListObject:0x3fe634d74498> JSON: {
  "object": "list",
  "has_before": false,
  "has_more": false,
  "total_count": 3,
  "data": [
    #<Octobat::Item id=oc_it_1460568443g3wu6b48fc3e 0x00000a> JSON: {
      "id": "oc_it_1460568443g3wu6b48fc3e",
      "object": "item",
      "transaction": "oc_txn_14605672518yko2fd30d23",
      "invoice": nil,
      "credit_note": nil,
      "tax_evidence": "oc_tev_1460565379am3be8f5ef71",
      "description": "Entreprise Plan",
      "unit_extratax_amount": 19900,
      "currency": "USD",
      "quantity": 1,
      "extratax_amount": 19900,
      "tax_rate": 22.0,
      "tax_amount": 4378,
      "gross_amount": 24278,
      "item_exchange": {
        "exchange_rate": 0.8864,
        "exchange_date": "2016-04-13T17:27:24.228Z",
        "exchanged_to_currency": "EUR"
      }
    },
    #<Octobat::Item[...] ...>,
    #<Octobat::Item[...] ...>
  ]
}
```


Returns a list of items.

### Returns
A hash with a data property that contains an array of items. Each entry in the array is a separate item object. If no items are available, the resulting array will be empty. This request should never raise an error.

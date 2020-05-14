![dynamicsplusplus](https://github.com/anderson-joyle/DynamicsPlusPlus/blob/master/DYNAMICS-logo.png)
Dynamics++ is a set of MSDYN365FO frameworks and utilities written in pure X++ (ideally).

## Find
Find methods are really usefull to select specific records. However, the approach of creating one/multiple find method(s) per table is not OOP driven.

#### DPPFind class
The goal of DPPFind class is provide a way to run select statements to fetch single records, filtering by field(s) or index.
Main methods are the following:
- **me**: Class entry point.
- **fromFields**: Select record based on containers of fields and parms. Both containers must have same number of elements. 'Find' classes will match field and value following container ordering e.g. conpeek(fields, i) == conpeek(parms, i).
- **fromIndex**: Select record based on table index name. Both index fields and parms must have same number of elements.
- **fromRecId**: For convenience. Calls **fromFields** method setting RecId field.
- **fromPrimary**: For convenience. Calls **fromIndex** method retrieving table primary key property.
- **verbose**: Print debug messages. Helpful when troubleshooting.
- **selectForUpdate**: Set found record as 'forupdate'.
- **get**: Fetch record.

**Example:**

```c#
public void test()
{
    CustTable custTable;
    InventTable inventTable;
    CustParameters parameters;
    
    // (...) where AccountNum == "C001"
    custTable = DPPFind::me(custTable).
                         fromPrimary(["C001"]).
                         get();
    
    // (...) where ItemType == ItemType::Item && ItemId == "INV001"
    inventTable = DPPFind::me(inventTable).
                              fromIndex(identifierStr("TypeIdx"), [ItemType::Item, "INV001"]).
                              get();
    
    // When table is a parameter table (TableGroup = Parameter) just call .get() method.
    parameters = DPPFind::me(parameters).
                          get();
                          
     // Do something else
}
```

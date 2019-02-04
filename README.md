# Dynamics++
Dynamics++ is a set of MSDYN365FO frameworks and utilities written in pure X++ (ideally).

## Find
Find methods are really usefull to select specific records. However, the approach of creating one/multiple find method(s) per table is not OOP driven.

#### DPPFind class
The goal of DPPFind class is provide a way to run select statements to fetch single records, filtering by field(s) or index.
Main methods are the following:

<i>Coming soon.</i> 

**Example:**

```c#
public void test()
{
    CustTable custTable;
    
    custTable = DPPFind::me(custTable).
                         fromPrimary(["C001"]).
                         get();
                         
    info(custTable.name());
}
```

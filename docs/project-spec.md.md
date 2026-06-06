A new program that uses Avalara API connections to download transactions. Currently transactions are imported into Eclipse by running a report on a web portal, downloading the report, extracting the data, importing the data in a Tab Delimited file. This is a labor intensive monthly process that I would like to change into an API pull at will.  
I’ve interfaced with Avalara before by API when developing the ECMS Sync. I wrote the programs for the APIs, and the Sync programs to interface with Avalara so these are examples of my coding style, as well as examples of how to interface between Eclipse and Avalara.

Avalara AvaTax is the integration we use and the API we use. I followed the C# SDK which appears to have changed significantly since I wrote these programs for using the API interface.

### Phase 1.

&nbsp;Get transactions for a time period, or a single transaction as needed. I would like to be able to download transactions for any period of time. Control programs will download transactions daily once live. I will also download transactions weekly for the entire MTD period, and one final time after the end of the month for all transactions in the previous month. These Avalara transaction details will be placed in the file AVALARA_PORTAL with the Doc ID (which is the same as the Eclipse file AR AR.ID or @ID) as the key. During the current month, transactions in Avalara are Uncommitted. There is a process that runs after month end to commit transactions in Avalara. These are the transactions that are Invoiced in the now closed month. For the current month we should download transactions according to the current month’s invoiced transactions. In other words, the Eclipse ERP will be the source of record IDs that are downloaded from Avalara. After month end, we will download ALL committed transactions to also identify any transactions that are in Avalara for a period and no longer in that period for Eclipse, or that are in that period in Eclipse, but not yet committed in Avalara. This will be to back up the Eclipse commit process in a later phase.

### Phase 2.

&nbsp;Reconcile transactions. Be certain that transactions are correct between the ERP system and the Avalara system, and overcome differences between the two. For example, it is valid to have a transaction in Eclipse without line items. It is not valid in Avalara AvaTax to have a transactions without line items. If the value of the transaction in Eclipse is 0.00 and there is no GL impact, then the program will cancel the transaction.

### Phase 3.

Proactive review of a transaction between Eclipse and Avalara at time of invoicing to insure that transactions are correctly taxed before the customer is sent an Invoice document. Sometimes the last tax call to Avalara fails and Eclipse will change a tax value to 0.00 when it is incorrect and not reflected in Avalara. Then we bill the customer for 0.00 in tax when we should have billed them for some amount of tax. We should be able to look up the transaction in Avalara, see that there is a difference, and re-calc the tax on that transaction (through a standard routine call in Eclipse).

Focus on phase 1 now, downloading transactions for manual reporting and comparison, and leave logical space for the remaining phases. Don’t write yourself into a corner where a full rearchitecture will be required to implement future phases.
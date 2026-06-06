REPO UD.AVA.ECMS.SYNC

API Call example programs  
UD.AVA.QUERYCUSTOMERS

- Returns a page of customers.  Calle from UD.AVA.PORT.CUSTS which handles paging.
- Good example for using the \$filter
- Good example of \$top, \$skip, and \$orderBy parameters.
- Example of logging to UD.AVALOG– Different log for each program/function.

&nbsp;

Calling an API call program  
UD.AVA.PORT.CUSTS

- Example of calling an API and processing the return data
- Example of nested data... not necessarily required in the new program, but useful to know it's available.
- Example of paging through large amounts of data returned by API.  Paging of data.
- Example of authenticating using COMPANY.ID based on Branch.  Branch is either GL.BRANCH from a transaction or the default branch.
- Example of logging to UD.AVALOG– Different log for each program/function.

&nbsp;

Process orchestration program  
UD.AVA.ECMS.SYNC

- Example of orchestrating the calls, and how the program runs based on schedule and timing.  
    - This can be useful when implementing a daily download/sync, vs weekly or Monthly.
- Example of logging to UD.AVALOG  -- Different log for each program/function.

&nbsp;

More recently coded program  
UD.PH.XOPEN.MSG

- Example of logging to a LAST.ACTION log
- Example of a Phantom run program (Phantom is generally a background run process), if needed.
- Another good example of reading SETUP from a .SETUP record stored in UD.CONTROL with tags, and using a default for the setting when a value isn't available in the .SETUP record
- Example of using the THREAD object for tracking the run.  NOT required.  Use it if useful in program.
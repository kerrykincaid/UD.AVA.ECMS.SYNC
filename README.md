# UD.AVA.ECMS.SYNC

API calls and programs to keep customer data synced between Eclipse and Avalara.

## **Background**

These programs all run on a Universe Pick Basic platform for the Eclipse DMS environment. Eclipse extends the Pick Basic language and a developer designed UD.COMPILE to extend Eclipse Pick Basic. Programs in OBP are Object Basic Programs. They are compiled by UD.COMPILE into Eclipse Pick Basic into the CBP directory. CBP is Customer Basic Programs. UD.CONTROL supports Objects that have been developed by the same developer, Don. This is affectionately referred to as .Don or Dot Don. OBP programs will have a corresponding CBP program. The difference is that the CBP Program is the program after it has passed through the UD.COMPILE compiler, or rather precompiler. There can be programs that are ONLY in CBP if they were written in native Eclipse Pick Basic, or Pick Basic.

Setup files are contained in the UD.CONTROL directory. They are referenced as Setup Object reference in the OBP files. They contain setup values for the programs. Flags, url snippets, variables for use in API calls. Mostly key value pairs.

&nbsp;

## **Purpose**

The purpose of these programs is to make API Calls from Eclipse to synchronize customer data between Eclipse and Avalara. Avalara used to have a file import/export system for this process known as ECMS. I'm still using that name for this process. Eclipse customer Sales Tax exemption information is extracted from the customer record, kept in an intermediate location (for comparison) and sent / received with Avalara via API calls. The Eclipse system natively uses Avalara for Sales Tax calculation, but doesn't natively sync customer certificate information with Avalara. These programs work together to close that gap.

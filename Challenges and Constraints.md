# Constraints and Technical Limitations
### 1. Live Workbook Requirement
Novatech Management requires the dashboard workbook to remain live and editable, allowing operational staff to update sales and invoice data on an ongoing basis. 
As a result, certain advanced Excel features could not be adopted.

#### Specifically:
- The common approach of using Power Query to automatically aggregate monthly files from a shared folder was not feasible in this setup, as Power Query is not available in Excel Online.
- Data ingestion therefore depends on manual copy-and-paste entry by staff into predefined monthly worksheets (Jan–Dec).

### 2. Data Aggregation Workaround

To consolidate the monthly data into a single dataset for reporting and pivoting, a formula-based approach was used.

Each month has its predefined sheet each with its own structured table (JAN, FEB, MAR,...Dec.). 
A central Summary sheet was used to aggregate all monthly tables using the VSTACK() function.

**Example formula used for aggregation:**

_=VSTACK(
  JAN[S/N], FEB[S/N], MAR[S/N], APR[S/N], MAY[S/N],
  JUN[S/N], JUL[S/N], AUG[S/N], SEP[S/N], OCT[S/N], NOV[S/N]
)_

This formula is repeated across all relevant columns to achieve a stacking of all the months' data into a single summary sheet

### 3. Compatibility Challenge

A major limitation of this approach is that the VSTACK() function is only available in Microsoft 365.

This introduces the following risks:

- If the management decides to open **AND** modify the workbook in older Excel versions (e.g., Excel 2016/2019) will result in formula errors.
Viewing only will not result in any errors.
- Long-term scalability and portability of the dashboard are constrained by version dependency.

**4. Mitigation Considerations**

To manage these limitations:

- Users are required to onoy modify the file using Microsoft 365.
- Monthly input sheets are standardized to reduce copy-and-paste errors.
- The dashboard design minimizes recalculation complexity to maintain performance despite formula-based aggregation.

### Summary

While the solution meets the requirement for a live, continuously updated dashboard, it involves trade-offs:

- Manual data entry instead of automated ingestion
- Dependency on Microsoft 365 due to VSTACK()
- Reduced portability across Excel versions

These constraints were accepted in order to deliver timely insights and enable management to make informed decisions on the proposed loyalty and incentive program.

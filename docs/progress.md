# Assignment 2: Business Intelligence Progress Log

This page records the practical development of the MaxMin Manufacturing multidimensional model. The project uses SQL Server as the relational source, SQL Server Analysis Services (SSAS) for the multidimensional cube, and Excel for the final OLAP analysis.

## Environment

- Database Engine: `JOY\SQLEXPRESS`
- Analysis Services: `JOY\SSAS2019`
- Manufacturing relational database: `MaxMinManufacturingDM`
- Analysis Services project: `MaxMinManufacturingDM`
- Cube: `Manufacturing`

## 1. Database Access and Source Verification

The SSAS service account was mapped to the Manufacturing database and granted the `db_datareader` and `public` database roles. This permits Analysis Services to read the source data while processing the cube.

![SSAS service account database permissions](screenshots/Picture1.png)

The Manufacturing product table was queried in SQL Server Management Studio to verify that the restored Manufacturing database was available and contained product data.

![Manufacturing product data query](screenshots/Picture2.png)

The supplied Sales database was also restored and queried. This confirms that the relational source required for the later Sales data-mining part of the assignment is available.

![Sales product data query](screenshots/Picture3.png)

## 2. Manufacturing Date Calculations

The `ManufacturingFact` table was explored through the Data Source View. Named calculations derived from `DateOfManufacture` produced Year, Quarter, and Month values for time-based analysis.

![Manufacturing fact data and named date calculations](screenshots/Picture4.png)

## 3. Manufacturing Time Dimension

A Manufacturing Time dimension was created from `DateOfManufacture`, with Day, Month, Quarter, and Year attributes.

![Manufacturing Time dimension attributes](screenshots/Picture5.png)

Attribute relationships were configured so that detailed dates roll up through Month and Quarter to Year.

![Time dimension attribute relationships](screenshots/Picture6.png)

The user-defined Calendar hierarchy was arranged in the browsing order Year, Quarter, Month, and Day.

![Calendar hierarchy](screenshots/Picture7.png)

## 4. Data Source View

The completed Data Source View contains `ManufacturingFact` and the related Batch, Product, Product Subtype, Product Type, Machine, Machine Type, Material, Plant, and Country dimension tables. The relationship chains support product, machine, material, plant, and country analysis.

![Completed Manufacturing Data Source View](screenshots/Picture8.png)

## 5. Cube Structure

The Manufacturing cube was created with `ManufacturingFact` as its measure group. The cube includes the Manufacturing Time, Product, Batch, and Machine dimensions.

![Manufacturing cube structure](screenshots/Picture9.png)

## 6. Product Dimension

The Product dimension was configured with the natural roll-up relationship Product to Product Subtype to Product Type. This supports the user-facing hierarchy Product Type, Product Subtype, and Product.

![Product dimension attribute relationships](screenshots/Picture10.png)

## 7. Machine Dimension

The Machine dimension contains hierarchies for machine/material analysis and plant geography. Manufacturer and Date of Purchase remain available as filtering attributes.

![Machine dimension hierarchies](screenshots/Picture11.png)

Attribute relationships support the roll-ups from Machine to Machine Type to Material and from Machine to Plant to Country.

![Machine dimension attribute relationships](screenshots/Picture12.png)

## 8. Dimension Usage

Dimension Usage was configured to connect Manufacturing Time, Product, Batch, and Machine to the Manufacturing Fact measure group at their corresponding granularity attributes.

![Cube dimension usage](screenshots/Picture13.png)

## 9. Calculated Measures

Two calculated measures were added to the cube:

- **Total Products** = Accepted Products + Rejected Products
- **Percent Rejected** = Rejected Products / Total Products, with division-by-zero protection

![Total Products and Percent Rejected calculations](screenshots/Picture14.png)

## 10. Deployment and Processing

The project was built, deployed, and processed on `JOY\SSAS2019`. The deployment completed successfully with zero errors. Non-blocking design warnings remain for final cleanup, including redundant visible attribute hierarchies and a recommendation to mark suitable relationships as rigid.

![Successful SSAS deployment](screenshots/Picture15.png)

## 11. Cube Validation

The cube browser returned the stored and calculated measures, confirming that the processed cube could be queried successfully.

![Overall Manufacturing cube measures](screenshots/Picture16.png)

The Product hierarchy was then used to analyse Accepted Products, Rejected Products, Total Products, Percent Rejected, and Elapsed Time for Manufacture by Product Type, Product Subtype, and Product.

![Manufacturing measures by Product hierarchy](screenshots/Picture17.png)

## Current Outcome

The Manufacturing multidimensional model is operational and supports product, batch, machine, geography, material, and calendar analysis. The cube calculates total production and rejection percentage and has been successfully deployed and queried.

The current warehouse contains overall `ElapsedTimeForManufacture`, but it does not contain separate molding, hardening, painting, or curing durations, or a paint-type attribute. Those business questions cannot be answered completely from the current schema and should be identified as data-collection gaps in the final feasibility report.

## Remaining Assignment Work

1. Complete the Excel OLAP workbook with clear PivotTables, filters, drill-down examples, and column charts.
2. Configure the supplied `MaxMinSalesDM` project for `JOY\SQLEXPRESS` and deploy it to `JOY\SSAS2019`.
3. Create Decision Trees, Naive Bayes, Clustering, and Neural Network mining models using the required customer filter and 50/50 training/testing split.
4. Produce and interpret the lift chart.
5. Complete the recommendations report and pair-practice log with selected evidence from this progress log.

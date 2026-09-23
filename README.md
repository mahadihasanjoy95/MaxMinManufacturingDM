# MaxMin Manufacturing BI Project

This README shows the main steps I completed while creating and testing the MaxMin Manufacturing SSAS cube.

## Database Setup

Granted the SSAS service account read access to the Manufacturing database.

![Database permissions](docs/screenshots/Picture1.png)

Checked the Manufacturing product data in SQL Server.

![Manufacturing database query](docs/screenshots/Picture2.png)

Checked that the supplied Sales database was also available.

![Sales database query](docs/screenshots/Picture3.png)

## Date Calculations and Time Dimension

Created Year, Quarter, and Month values from `DateOfManufacture`.

![Named date calculations](docs/screenshots/Picture4.png)

Created the Manufacturing Time dimension with Day, Month, Quarter, and Year attributes.

![Time dimension attributes](docs/screenshots/Picture5.png)

Configured the time attribute relationships.

![Time attribute relationships](docs/screenshots/Picture6.png)

Created the Calendar hierarchy from Year to Day.

![Calendar hierarchy](docs/screenshots/Picture7.png)

## Data Source View and Cube

Added the fact, dimension, and lookup tables and verified their relationships.

![Data Source View](docs/screenshots/Picture8.png)

Created the Manufacturing cube with Time, Product, Batch, and Machine dimensions.

![Cube structure](docs/screenshots/Picture9.png)

## Product and Machine Dimensions

Configured Product, Product Subtype, and Product Type relationships.

![Product relationships](docs/screenshots/Picture10.png)

Created the Machine/Material and Plant Geography hierarchies.

![Machine hierarchies](docs/screenshots/Picture11.png)

Configured the Machine, Machine Type, Material, Plant, and Country relationships.

![Machine relationships](docs/screenshots/Picture12.png)

## Measures and Deployment

Connected the Time, Product, Batch, and Machine dimensions to the Manufacturing Fact measure group.

![Dimension usage](docs/screenshots/Picture13.png)

Created the Total Products and Percent Rejected calculated measures.

![Calculated measures](docs/screenshots/Picture14.png)

Built, deployed, and processed the cube successfully.

![Successful deployment](docs/screenshots/Picture15.png)

## Cube Results

Checked the stored and calculated measure totals in the cube browser.

![Cube totals](docs/screenshots/Picture16.png)

Viewed the measures by Product Type, Product Subtype, and Product.

![Product hierarchy results](docs/screenshots/Picture17.png)

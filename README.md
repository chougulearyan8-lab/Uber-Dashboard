# Uber Ride Booking & Business Performance Dashboard

A Power BI project for exploring Uber ride-booking activity, vehicle performance, revenue, cancellations, customer behaviour, and service ratings.

> **Project file:** `Uber.pbix`  
> **Primary tool:** Microsoft Power BI  
> **Data preparation:** Power Query Editor  
> **Analytics:** Power BI data modelling and DAX  
> **Report pages:** Home, Overall, Vehicle Type, Revenue, Cancellation, and Ratings

---

## Table of Contents

- [Project Overview](#project-overview)
- [Project Objectives](#project-objectives)
- [Dataset Overview](#dataset-overview)
- [Tools and Technologies](#tools-and-technologies)
- [Project Workflow](#project-workflow)
- [1. Data Preparation in Power Query Editor](#1-data-preparation-in-power-query-editor)
- [2. Data Modelling](#2-data-modelling)
- [3. DAX Measures and Calculations](#3-dax-measures-and-calculations)
- [Dashboard Walkthrough](#dashboard-walkthrough)
  - [Home Page](#1-home-page)
  - [Overall Analysis](#2-overall-analysis)
  - [Vehicle Type Analysis](#3-vehicle-type-analysis)
  - [Revenue Analysis](#4-revenue-analysis)
  - [Cancellation Analysis](#5-cancellation-analysis)
  - [Ratings Analysis](#6-ratings-analysis)
- [Filters and Interactivity](#filters-and-interactivity)
- [Business Questions Answered](#business-questions-answered)
- [Key Analytical Takeaways](#key-analytical-takeaways)
- [How to Open the Project](#how-to-open-the-project)
- [Limitations and Notes](#limitations-and-notes)
- [Future Enhancements](#future-enhancements)

---

## Project Overview

The **Uber Ride Booking & Business Performance Dashboard** is an interactive Power BI report designed to analyse ride-booking operations from multiple business perspectives.

A ride-booking business needs to understand more than the number of rides requested. It also needs to monitor how many bookings are completed, how many are cancelled, which vehicle categories are used, how revenue is distributed across payment methods, how far customers travel, and how customers rate the service.

This report brings these topics together in one place. It uses summary cards, time-series charts, pie charts, column charts, and a customer table to make operational and commercial patterns easier to explore.

The report contains six pages:

1. **Home Page** – landing and navigation page.
2. **Overall** – booking volume and booking-status overview.
3. **Vehicle Type** – comparison of booking value, ride distance, and booking outcomes by vehicle category.
4. **Revenue** – payment-method revenue, ride-distance distribution, and top customers.
5. **Cancellation** – booking success, cancellations, cancellation rate, and reasons for cancellations.
6. **Ratings** – customer and driver rating information by vehicle category.

## Project Objectives

The main objectives are to:

- Monitor total ride bookings and booking activity over time.
- Understand the distribution of booking statuses.
- Compare performance across vehicle types.
- Examine booking value and revenue by payment method.
- Explore ride-distance patterns.
- Identify customers contributing the highest booking value.
- Monitor successful and cancelled bookings.
- Understand customer-side and driver-side cancellation reasons.
- Review customer and driver ratings across vehicle categories.
- Provide an interactive report that supports date-based analysis.

## Dataset Overview

The report uses a ride-booking dataset whose model table is identified in the report metadata as `ncr_ride_bookings`.

The report references fields including:

| Field | Analytical purpose |
|---|---|
| `Booking ID` | Identifies a booking and supports booking counts. |
| `Date` | Supports date filtering and time-based analysis. |
| `Month` | Supports monthly grouping in visuals. |
| `Booking Status` | Separates booking outcomes, such as successful and cancelled bookings. |
| `Booking Value` | Represents the monetary value associated with a booking. |
| `Vehicle Type` | Enables comparisons between vehicle categories. |
| `Ride Distance` | Supports analysis of trip-distance patterns. |
| `Payment Method` | Enables revenue comparisons by payment method. |
| `Customer ID` | Identifies customers and supports customer-level analysis. |
| `Customer Rating` | Represents the customer's rating information. |
| `Driver Ratings` | Represents driver-rating information. |
| `Reason for cancelling by Customer` | Describes customer-side cancellation reasons. |
| `Driver Cancellation Reason` | Describes driver-side cancellation reasons. |
| `Cancelled Rides by Customer` | Supports customer cancellation analysis. |
| `Cancelled Rides by Driver` | Supports driver cancellation analysis. |

The table above lists fields referenced by report visuals. It is not intended to be a complete inventory of every column in the underlying source dataset.

---

## Tools and Technologies

| Tool / Technology | How it is used |
|---|---|
| Microsoft Power BI Desktop | Report creation, visualisation, and interactive analysis. |
| Power Query Editor | Data cleaning and preparation before reporting. |
| Power BI Data Model | Organising fields and calculations for analysis. |
| DAX (Data Analysis Expressions) | Creating analytical calculations and measures. |
| `.pbix` | Power BI report/project file format. |
| Markdown | Project documentation in this README. |

---

## Project Workflow

The project follows this general sequence:

```text
Source Ride-Booking Dataset
          |
          v
Power Query Editor
          |
          v
Data Cleaning and Transformation
          |
          v
Apply and Load Prepared Data
          |
          v
Data Modelling
          |
          v
Create DAX Measures
          |
          v
Build Dashboard Visuals
          |
          v
Add Filters and Navigation
          |
          v
Analyse Business Performance
```

The data is prepared before it is used in the report. The model then provides the fields and calculations required by the dashboard visuals.

## 1. Data Preparation in Power Query Editor

Power Query Editor is the data preparation and transformation environment in Power BI. It is used to inspect the source data, correct data-quality issues, and prepare columns for analysis before loading the result into the model.

For this project, the dataset was cleaned in Power Query Editor before dashboard development.

### Why data cleaning is important

A dashboard is only as reliable as the data behind it. Inconsistent dates, incorrect data types, blank identifiers, duplicate records, or inconsistent category labels can lead to misleading totals and comparisons.

The cleaning stage should make sure that:

- Columns have appropriate data types.
- Date fields can be used for time-based reporting.
- Numeric fields can be aggregated correctly.
- Categories use consistent labels.
- Missing or invalid values are handled appropriately.
- Booking identifiers are suitable for counting and analysis.

### Typical Power Query preparation checks

The following describes the data-preparation checks relevant to this type of report. It is a documentation of the appropriate workflow, not a verified list of the exact Power Query steps applied in the uploaded file.

#### 1. Inspect the source data

The source table is reviewed in Power Query Editor to understand its structure, column names, data types, and the meaning of the available fields.

This helps identify which fields are identifiers, dates, categories, numeric values, ratings, and cancellation descriptions.

#### 2. Set appropriate data types

Each field should use a data type that matches its purpose.

Examples:

- `Booking ID` and `Customer ID`: identifier/text fields, depending on the source format.
- `Date`: Date or Date/Time.
- `Booking Value`: Decimal Number or Fixed Decimal Number.
- `Ride Distance`: Decimal Number.
- `Customer Rating` and `Driver Ratings`: numeric fields.
- `Booking Status`, `Vehicle Type`, and `Payment Method`: Text.

Correct data types are important because Power BI uses them to determine how fields can be filtered, sorted, grouped, and aggregated.

#### 3. Review missing and blank values

Blank values should be inspected in important fields.

For example:

- A missing booking identifier can affect booking counts.
- A missing booking date can prevent a record from appearing in date-based analysis.
- A missing payment method may affect payment-method reporting.
- A missing cancellation reason may be expected for a completed ride, so it should not automatically be treated as an error.

Missing values should be handled according to the business meaning of the field rather than replaced indiscriminately.

#### 4. Check duplicate records

Booking identifiers can be used to investigate duplicate bookings.

However, duplicate removal should only be performed when the records are genuinely duplicate source records. Multiple rows with the same identifier may sometimes represent a valid data structure, so the source's row-level meaning should be understood first.

#### 5. Standardise categorical values

Text categories should be reviewed for inconsistent spelling, capitalisation, and unwanted spaces.

Fields that benefit from this check include:

- `Booking Status`
- `Vehicle Type`
- `Payment Method`
- Cancellation-reason fields

For example, values that represent the same status should use one consistent label. Otherwise, a chart may show separate categories for what is actually the same business outcome.

#### 6. Validate numeric fields

Numeric columns such as `Booking Value`, `Ride Distance`, and rating fields should be checked for invalid or unexpected values.

Examples of useful checks:

- Booking values should be interpreted using the correct currency and decimal precision.
- Ride distances should use a consistent unit.
- Ratings should follow the rating scale used by the source.
- Unexpected negative or out-of-range values should be investigated rather than silently changed.

#### 7. Prepare date fields for reporting

The `Date` field is important because the report includes date slicers and a ride-volume trend.

Dates should be stored as valid date values. The `Month` field is also referenced by the report's revenue visuals.

For a more advanced model, a separate calendar table can be created and related to the booking table.

#### 8. Apply the transformations

After checking the data and applying the required transformations, the prepared data is applied and loaded into the Power BI model.

**Result:** The report can use prepared fields for booking, revenue, vehicle, cancellation, distance, and rating analysis.

> To make this section an exact transformation log, add the actual Applied Steps shown in Power Query Editor (for example, the specific rename, replace, remove, split, or type-conversion operations used in your query).

## 2. Data Modelling

Data modelling organises the prepared data so that Power BI visuals and calculations can work together consistently.

The report metadata identifies a booking table named `ncr_ride_bookings`. The report visuals use fields from this table for booking, date, vehicle, revenue, customer, cancellation, and rating analysis.

### Fields and their roles

The model uses different types of fields:

- **Identifiers:** `Booking ID` and `Customer ID`.
- **Date fields:** `Date` and `Month`.
- **Categorical fields:** `Booking Status`, `Vehicle Type`, and `Payment Method`.
- **Numeric fields:** `Booking Value`, `Ride Distance`, and rating fields.
- **Descriptive fields:** customer and driver cancellation reasons.

### Why modelling matters

A well-organised model helps:

1. Keep calculations consistent across report pages.
2. Apply filters to the correct visuals.
3. Support comparisons across dates and categories.
4. Separate descriptive categories from numeric values.
5. Make the report easier to maintain and extend.

### Recommended model improvements

For a larger or more advanced version of this project, consider:

- Creating a dedicated calendar table.
- Relating the calendar table to the booking date.
- Creating separate dimension tables for vehicle type, payment method, and booking status where appropriate.
- Defining clear relationships and checking their filter directions.
- Hiding technical columns that report users do not need.
- Giving measures descriptive names and documenting their business definitions.

These are recommendations for model development; the uploaded report does not provide enough information to verify whether separate dimension tables or a calendar table were created.

## 3. DAX Measures and Calculations

DAX (Data Analysis Expressions) is the formula language used by Power BI for analytical calculations.

Measures are evaluated in the current filter context. This means a measure can return different results when a user selects a different date, vehicle type, payment method, or other category.

The uploaded report explicitly references a measure named:

- `CanceledPercentage`

It is used by the **Cancellation Rate** card on the Cancellation page.

The report also uses booking counts and aggregations of booking value, ride distance, and ratings in its visuals. Some of these appear as visual-level aggregations of columns rather than named DAX measures.

### Cancellation percentage

The business concept represented by `CanceledPercentage` is the proportion of bookings that were cancelled.

A common definition is:

\[
\text{Cancellation Rate} =
\frac{\text{Cancelled Bookings}}{\text{Total Bookings}}
\times 100
\]

An illustrative DAX pattern is:

```dax
Total Bookings =
DISTINCTCOUNT(ncr_ride_bookings[Booking ID])
```

```dax
Cancelled Bookings =
CALCULATE(
    [Total Bookings],
    ncr_ride_bookings[Booking Status] = "Canceled"
)
```

```dax
CanceledPercentage =
DIVIDE(
    [Cancelled Bookings],
    [Total Bookings],
    0
)
```

Format the percentage measure as a percentage in Power BI if the formula returns a decimal ratio.

**Important:** These formulas explain a standard implementation of the calculation. The exact DAX definition and cancellation-status spelling in the uploaded semantic model could not be verified. The report metadata confirms the measure name `CanceledPercentage`, but does not expose its formula.

### Other useful measures for extending the report

The following are examples of additional measures that can be created if they are not already present:

```dax
Successful Bookings =
CALCULATE(
    [Total Bookings],
    ncr_ride_bookings[Booking Status] = "Success"
)
```

```dax
Total Booking Value =
SUM(ncr_ride_bookings[Booking Value])
```

```dax
Average Ride Distance =
AVERAGE(ncr_ride_bookings[Ride Distance])
```

```dax
Average Customer Rating =
AVERAGE(ncr_ride_bookings[Customer Rating])
```

```dax
Average Driver Rating =
AVERAGE(ncr_ride_bookings[Driver Ratings])
```

Check the exact status labels and column names in the source model before using these examples. They are suggested extensions, not claims about measures already created in the project.

---

# Dashboard Walkthrough

This section explains the purpose of each report page, the visuals identified in the PBIX, and how a business user can interpret them.

## 1. Home Page

The Home Page is the landing page of the report.

It contains an action/navigation button and serves as the starting point for exploring the report.

### Purpose

- Provide an entry point to the dashboard.
- Help users move into the analytical pages.
- Give the report a clear navigation structure.

### How to use it

Open the report and use its navigation control to move to the required analysis page. The other pages provide detailed views of bookings, vehicle types, revenue, cancellations, and ratings.

## 2. Overall Analysis

The Overall page gives a high-level view of ride-booking activity.

It combines a booking-volume trend, booking-status breakdown, a total-bookings card, and a date slicer.

### Visuals on this page

#### Total Bookings

A card displays the total booking count based on `Booking ID`.

**Business value:** This gives users a headline measure of booking activity for the selected reporting period.

When the date selection changes, the displayed total can be used to examine activity within the selected period, subject to the model's filter configuration.

#### Ride Volume Over Time

A line chart displays booking volume over time using the booking identifier and the report's date-based analysis.

**What it helps explain:**

- How booking activity changes over the selected period.
- Whether activity is relatively stable or fluctuates.
- Which periods show higher or lower booking volumes.
- Whether there are recurring peaks or declines worth investigating.

**Business use:** Operations teams can use booking trends as a starting point for understanding demand patterns and planning service capacity.

#### Booking Status Breakdown

A pie chart shows the distribution of `Booking Status`.

**What it helps explain:**

- How bookings are distributed among their recorded statuses.
- The relative contribution of successful and cancelled outcomes.
- Whether one status represents a large share of booking activity.

**Business use:** This provides an at-a-glance view of the booking funnel's outcomes. It can also help identify whether cancellations deserve deeper investigation on the Cancellation page.

#### Date Slicer

The date slicer uses the `Date` field.

Users can select a reporting period to investigate booking activity within a chosen date range.

### Questions answered

- How many bookings were recorded?
- How does booking volume change over time?
- What is the distribution of booking statuses?
- How does the overview change when a different date range is selected?

## 3. Vehicle Type Analysis

The Vehicle Type page compares booking-related metrics across vehicle categories.

The report contains multiple card visuals using `Vehicle Type` together with `Booking Value`, `Ride Distance`, and, in some cards, `Booking Status`. It also includes a date slicer.

### Main analytical dimensions

#### Booking Value by Vehicle Type

Cards use booking value and vehicle type to present category-level booking-value information.

**What it helps explain:**

- How booking value differs between vehicle categories.
- Which vehicle categories contribute more or less booking value.
- How the selected date range affects the comparison.

**Business use:** This can support analysis of the commercial contribution of different vehicle categories.

#### Ride Distance by Vehicle Type

Cards use ride distance and vehicle type to compare distance-related information.

**What it helps explain:**

- How ride-distance patterns vary by vehicle category.
- Whether some categories are associated with different trip-distance profiles.
- Which vehicle categories may need further investigation by distance segment.

**Business use:** Distance patterns can help inform fleet planning, service design, and category-level operational analysis.

#### Booking Status by Vehicle Type

Some card visuals also use booking status alongside vehicle type and booking value.

**What it helps explain:**

- How booking outcomes can be examined within vehicle categories.
- Whether category-level booking performance changes across the selected period.

The precise aggregation and individual card titles are not exposed clearly in the report metadata, so the cards should be inspected in Power BI to confirm whether each displays a sum, average, count, or another aggregation.

#### Date Slicer

The date slicer allows the vehicle analysis to be restricted to a selected period.

### Questions answered

- How do vehicle categories compare?
- How does booking value vary by vehicle type?
- How do ride distances differ across vehicle categories?
- How can booking outcomes be examined by vehicle category?

## 4. Revenue Analysis

The Revenue page focuses on booking value, payment methods, ride distance, and customer contribution.

It contains a column chart for revenue by payment method, a ride-distance distribution chart, a Top 5 Customers table, and a date slicer.

### Visuals on this page

#### Revenue by Payment Method

A column chart compares `Booking Value` across `Payment Method` categories.

**What it helps explain:**

- Which payment methods account for more booking value.
- How booking value is distributed across payment categories.
- How the payment-method pattern changes when the date filter changes.

**Business use:** This can help business teams understand payment-method usage and the relative monetary contribution associated with each method.

**Interpretation note:** The exact aggregation configured in the visual should be checked in Power BI. A sum of booking value represents total booking value, while an average would represent average booking value per record. These interpretations are not interchangeable.

#### Ride Distance Distribution

A column chart titled **Ride Distance Distribution** uses `Ride Distance` and includes month and payment-method fields in its visual query.

**What it helps explain:**

- How ride-distance information is distributed in the report.
- How distance patterns can be explored across monthly and payment-method categories, depending on the visual's configured axis and legend.
- Whether the selected reporting period changes the observed distance pattern.

**Business use:** Ride-distance analysis can support investigation of trip patterns and the relationship between trip characteristics and commercial activity.

#### Top 5 Customers

A table titled **Top 5 Customers** uses `Customer ID`, `Booking Value`, and month-related information.

**What it helps explain:**

- Which customers appear at the top of the report's customer-value ranking.
- How booking value is associated with customer records.
- How the displayed customer information changes with the selected date range.

**Business use:** This can help identify high-value customer segments for further analysis.

The exact ranking aggregation and whether the table uses total booking value or another calculation should be confirmed in the visual's configuration.

#### Date Slicer

The date slicer allows users to examine revenue and customer information for a selected period.

### Questions answered

- How is booking value distributed by payment method?
- What ride-distance patterns are visible?
- Which five customers rank highest in the displayed customer table?
- How do these patterns change over time?

## 5. Cancellation Analysis

The Cancellation page focuses on booking outcomes and the reasons behind cancellations.

This page is especially useful for understanding service friction and identifying areas where operational improvements may be needed.

### KPI cards

#### Total Bookings

Displays the total number of bookings using `Booking ID`.

This provides the overall booking count for the current filter context.

#### Success Bookings

Displays bookings filtered by `Booking Status`.

This KPI represents the successful-booking count in the report.

#### Cancelled Bookings

Displays bookings filtered by `Booking Status`.

This KPI represents the cancelled-booking count in the report.

#### Cancellation Rate

Displays the `CanceledPercentage` measure.

This expresses cancellations relative to the total booking count, according to the measure's DAX definition.

A lower cancellation rate can indicate fewer cancelled bookings relative to total bookings, but the business should also investigate the reasons for cancellation rather than interpreting the rate alone.

### Cancellation charts

#### Cancelled Rides by Customers

A pie chart analyses customer-side cancellations using:

- `Reason for cancelling by Customer`
- `Cancelled Rides by Customer`

**What it helps explain:**

- Which customer cancellation reasons are represented in the data.
- How customer-side cancellations are distributed across reasons.
- Which reasons may deserve further investigation.

**Business use:** The business can use this information to investigate customer experience issues, booking friction, or service-related concerns.

#### Cancelled Rides by Drivers

A pie chart analyses driver-side cancellations using:

- `Driver Cancellation Reason`
- `Cancelled Rides by Driver`
- `Booking Status`

**What it helps explain:**

- Which driver-side cancellation reasons occur in the dataset.
- How driver cancellations are distributed across recorded reasons.
- Which reason categories contribute more prominently to driver-side cancellations.

**Business use:** Operations teams can investigate recurring driver-side cancellation reasons and consider whether scheduling, availability, communication, or other operational processes need attention.

### Date Slicer

The date slicer allows the user to investigate cancellation metrics and reasons over a selected period.

### Questions answered

- How many bookings were made?
- How many bookings were successful?
- How many bookings were cancelled?
- What percentage of bookings were cancelled?
- Why do customers cancel?
- Why do drivers cancel?
- How do cancellation patterns change across the selected dates?

### Why cancellation analysis matters

A cancellation is not just a lost booking. It can also indicate a problem in the booking experience or service operation.

Separating customer-side and driver-side cancellation reasons is useful because the two groups may require different business responses.

For example, customer-side reasons may need to be investigated from the perspective of customer experience, while driver-side reasons may need to be investigated from the perspective of driver operations.

The report helps identify where further investigation should begin; it does not by itself establish the cause of a cancellation.

## 6. Ratings Analysis

The Ratings page focuses on customer and driver ratings across vehicle categories.

The page contains multiple card visuals using `Customer Rating` and `Driver Ratings`, grouped by `Vehicle Type`.

### Customer Rating by Vehicle Type

The customer-rating cards use:

- `Customer Rating`
- `Vehicle Type`

**What it helps explain:**

- How customer-rating information varies across vehicle categories.
- Whether some vehicle categories have different rating patterns.
- Which categories may need further service-quality investigation.

**Business use:** Customer ratings can provide an indication of the customer experience associated with different vehicle categories.

### Driver Ratings by Vehicle Type

The driver-rating cards use:

- `Driver Ratings`
- `Vehicle Type`

**What it helps explain:**

- How driver-rating information varies across vehicle categories.
- Whether rating patterns differ between categories.
- Which categories may need additional operational review.

**Business use:** Driver-rating information can help the business examine service quality and identify areas for further review.

### Questions answered

- How do customer ratings vary by vehicle category?
- How do driver ratings vary by vehicle category?
- Are there differences in rating patterns between vehicle categories?
- Which categories may benefit from additional investigation?

The individual card titles and exact rating aggregations are not clearly available in the report metadata. Confirm whether each card displays an average or another aggregation in Power BI before quoting specific rating values.

---

## Filters and Interactivity

The report includes a `Date` slicer on the Overall, Vehicle Type, Revenue, and Cancellation pages.

A date slicer lets the user change the reporting period without manually rebuilding the visuals.

For example, a user can select a period and then investigate:

- Booking volume in the Overall page.
- Vehicle-category metrics in the Vehicle Type page.
- Payment-method and customer information in the Revenue page.
- Cancellation counts and reasons in the Cancellation page.

The effect of a slicer depends on the relationships and visual interactions configured in the Power BI model. Check the report's Edit interactions settings if a visual does not respond as expected.

The Ratings page contains category-based cards. The uploaded report metadata does not establish that every page has a date slicer.

## Business Questions Answered

The dashboard brings together several business questions:

| Business area | Example question | Relevant page |
|---|---|---|
| Booking activity | How many bookings are recorded? | Overall |
| Booking trends | How does ride volume change over time? | Overall |
| Booking outcomes | What is the booking-status distribution? | Overall |
| Vehicle performance | How do vehicle categories compare? | Vehicle Type |
| Commercial performance | How is booking value distributed by payment method? | Revenue |
| Trip patterns | What ride-distance patterns are visible? | Revenue |
| Customer contribution | Which customers appear in the Top 5 table? | Revenue |
| Cancellation performance | What is the cancellation rate? | Cancellation |
| Cancellation reasons | Why do customers and drivers cancel? | Cancellation |
| Service quality | How do customer and driver ratings vary by vehicle type? | Ratings |

## Key Analytical Takeaways

The report is designed to support the following types of analysis:

1. **Demand monitoring:** Use the booking trend to identify periods of higher or lower activity.
2. **Booking-outcome monitoring:** Use the booking-status breakdown and cancellation KPIs to understand booking outcomes.
3. **Vehicle-category comparison:** Compare booking value and ride-distance information across vehicle types.
4. **Payment analysis:** Examine how booking value is distributed across payment methods.
5. **Customer analysis:** Use the Top 5 Customers table to investigate customer-level booking value.
6. **Cancellation investigation:** Separate customer-side and driver-side reasons instead of treating every cancellation as the same issue.
7. **Service-quality review:** Compare customer and driver rating information across vehicle categories.

These are analytical opportunities provided by the report. Actual business findings—such as the highest-performing vehicle type, most-used payment method, or leading cancellation reason—should be written only after reviewing the live visual values and the selected date range.

---

## How to Open the Project

1. Install or open **Microsoft Power BI Desktop**.
2. Open the `Uber.pbix` file.
3. If Power BI asks for access to the semantic model or a sign-in, use an account that has the required permissions.
4. Wait for the report to load.
5. Use the page navigation controls to explore the dashboard.
6. Use the available date slicers to change the analysis period.
7. Select individual visuals to explore cross-filtering and interactions, where configured.

### Important connection note

The uploaded PBIX contains a connection reference to a remote Power BI semantic model. It does not appear to contain a self-contained copy of the full model and its source-query definitions.

Another user may therefore need access to the connected semantic model to view or refresh the report successfully.

## Limitations and Notes

- The report file confirms the six page names and the visuals and fields described in this README.
- The model table is identified as `ncr_ride_bookings`.
- The report references the DAX measure `CanceledPercentage`, but its exact formula is not exposed in the uploaded report metadata.
- The exact Power Query Applied Steps and M code are not available in the uploaded report package.
- The exact aggregation used by every card and chart should be confirmed in Power BI before publishing numerical conclusions.
- The dashboard's actual KPI values are not reproduced here because they can change with the semantic model, filters, and reporting period.
- The README describes the visible report structure and the intended analytical interpretation; it does not claim to verify every transformation performed in the original Power Query session.

## Future Enhancements

The dashboard could be extended with:

- A dedicated calendar table and additional time-intelligence measures.
- Month-over-month and year-over-year booking comparisons.
- Revenue trends over time.
- Average booking value and average ride-distance KPIs.
- Vehicle-type ranking by booking count and booking value.
- A customer-level booking-frequency analysis.
- A more detailed cancellation-rate breakdown by vehicle type and date.
- A cancellation-reason trend over time.
- Rating distributions and average-rating KPIs.
- Drill-through pages for customer or vehicle-category analysis.
- Dynamic titles that display the currently selected date range.
- Tooltips with additional KPI definitions and contextual information.
- A data dictionary documenting every source column and its business meaning.

---

## Conclusion

The Uber Ride Booking & Business Performance Dashboard provides a consolidated view of booking activity, vehicle categories, revenue, cancellations, and ratings.

The project demonstrates a complete Power BI reporting workflow:

1. Prepare and clean the dataset using Power Query Editor.
2. Organise the prepared data in the Power BI model.
3. Create analytical calculations using DAX.
4. Build visuals that answer business questions.
5. Add date filtering and report navigation.
6. Use the dashboard to explore operational and commercial performance.

The result is an interactive report that helps users move from raw ride-booking records to structured business analysis.

---

**Project:** Uber Ride Booking & Business Performance Dashboard  
**File:** `Uber.pbix`  
**Documentation:** `README.md`

Uber Ride Analytics Dashboard (Power BI)

An interactive Power BI report analyzing Uber ride booking data — covering ride completion rates, cancellations, revenue, distance, and vehicle-type performance, with a custom image-based vehicle slicer.

Report Pages

1. Home
Landing page with a welcome banner and page navigator to move into the report.

2. Overview
The main analytics page, including:


KPI cards: Completed Bookings, Lost/Cancelled Bookings, Revenue, Total Distance
KPI cards for Pickup Location and Drop Location (filtered to completed rides)
An image-based vehicle type slicer (Auto, Bike, Go Mini, Go Sedan, Premier Sedan, Uber XL) with custom vehicle icons
A date-axis slicer for time filtering
Area chart: Completed bookings trend by month
100% stacked column chart: Booking value by month
Clustered bar chart: Revenue by vehicle type
Three donut charts: Completed / Cancelled / Incomplete ride breakdowns


Data Model

TablePurposeUberFact table — Booking ID, Booking Status, Booking Value, Customer ID, Customer Rating, Driver Ratings, Pickup/Drop Location, Payment Method, Ride Distance, Vehicle Type, Date, cancellation reasons, etc.CalenderDate dimension table (Date, Month, MonthIndex, Quarter, QuarterIndex) for time intelligenceImageLookup table mapping each Vehicle Type to an image URL, used to power the custom image slicer_MeasureDedicated measures table holding all DAX calculations

Relationships:


Calender[Date] (1) → Uber[Date] (many)
Image[Vehicle Type] (1) → Uber[Ve_Type] (many) — drives the image slicer


Key Measures


Booking_Count — base row count measure
COMPLETED_BOOKING — count/value of successfully completed rides
LOST_BOOKING — count/value of cancelled or incomplete rides
Revenue — total booking revenue
Total_Distance — sum of ride distance
BOOKING_REMOVE_STATUS_FILTER — CALCULATE([Booking_Count], ALL(Uber[Booking Status])), used to show total bookings regardless of status filter (denominator for the donut charts' completion/cancellation/incomplete rate)


Notable Feature: Image-Based Vehicle Slicer

Instead of a plain text/list slicer, vehicle types are displayed as tappable icons (auto-rickshaw, bike, sedan, etc.). This is built by:


A separate Image table storing one row per vehicle type with an image URL (hosted on ibb.co)
An Advanced Slicer visual bound to Image[Vehicle Type], with Format Visual → Image → Field set to Image[Img]
A relationship from Image to Uber so slicer selections filter the fact table correctly


Tools Used


Power BI Desktop
DAX for measures and calculated columns
Power Query for data shaping

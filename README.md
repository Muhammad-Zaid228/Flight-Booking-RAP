# RAP Flight Booking Application (Z_SBOOK)

A modern RESTful ABAP Programming (RAP) application for managing flight booking data, built on the SAP BOPF framework and exposed as an OData V4 service.

## Prerequisites

### Mandatory System Environment
*   **SAP System:** SAP S/4HANA 2022 or SAP BTP, ABAP Environment (Steampunk)
*   **ABAP Platform Release:** 1909 or higher (2020+ recommended for full OData V4 feature support)
*   **Development IDE:** ABAP Development Tools (ADT) in Eclipse (Latest version)

## Installation & Activation

### 1. Import and Activate Objects
Activate all development objects in **exactly this sequence** using **ABAP in Eclipse (ADT)**:

1.  **Persistence Layer:**
    *   Database Table: `ZMY_A_SBOOK` (Base table)

2.  **Business Object Layer:**
    *   Data Definitions (CDS Views):
        *   `Z_CDS_L_SBOOK` (Root Leaf View)
        *   `Z_CDS_C_SBOOK` (Projection View)
    *   Behavior Definition: `Z_CDS_L_SBOOK` (for root entity)
    *   Behavior Implementation Class: `ZBP_CDS_L_SBOOK`

3.  **Consumption Layer:**
    *   Behavior Definition Projection: `Z_CDS_C_SBOOK`
    *   Metadata Extension: `Z_CDS_C_SBOOK` (UI annotations)

4.  **Service Layer:**
    *   Service Definition: `Z_UI_SBOOK`
    *   Service Binding: **Create Manually** (See Step 2)

5.  **Utilities:**
    *   Data Generation Class: `ZCL_DATA_CREATE_Z_A_SBOOK` (Optional, for test data)

### 2. Create and Publish the Service Binding

**This is a crucial manual step:**
1.  In ADT, right-click your package and select **New > Other ABAP Repository Object**.
2.  Navigate to **Service Development > Service Binding**.
3.  Enter the name `Z_UI_SBOOK_####` (or similar) and a description.
4.  Click **Next** and finish the creation.
5.  In the opened Service Binding editor, click **Add**.
6.  Select the Service Definition `Z_UI_SBOOK`.
7.  Set the **Binding Type** to **OData V4 - UI**.
8.  Activate the Service Binding.
9.  Select the newly added entity set and click **Publish** to expose it as a local service.

## Testing the Application

You can test the application through several channels:

### 1. OData Service Directly
*   Use the **SAP Gateway Client** (/n/IWFND/GW_CLIENT)
*   Use the **Service Binding Test Double-Click** in ADT (launches a Fiori Elements preview)

### 2. Fiori Elements App Preview
*   The Metadata Extension (`Z_CDS_C_SBOOK`) contains UI annotations.
*   After publishing the Service Binding, a basic Fiori Elements List Report/Object Page app is automatically generated.
*   Access it via the URL generated in the Service Binding preview.

### 3. Test Data Creation (Optional)
*   The utility class `ZCL_DATA_CREATE_Z_A_SBOOK` can be executed to generate sample flight bookings.
*   Run the class in ABAP (F9) or create a test program to call its public methods.

# Sales Invoice UI

A web-based sales invoice management application built using Blazor Web App (.NET 10).

The application provides a user-friendly interface for creating, viewing, editing, and deleting sales invoices. It communicates with a separate ASP.NET Core Minimal API backend and uses SQL Server for data storage through the API.

**Backend Repository:** [SalesInvoiceAPI](https://github.com/RamyBarakat01/SalesInvoiceAPI)

## Features

### Invoice Creation
- Select an existing customer or create a new customer.
- Select products and specify quantities.
- Add or remove product lines before creating an invoice.
- Apply percentage discounts to individual items.
- Apply a percentage discount to the entire invoice.
- Preview subtotals, discounts, and the final invoice amount.
- Automatically round the final invoice total down to the nearest whole EGP.

### Invoice Details and Editing
- Search for invoices by ID.
- Display invoice information, purchased products, and totals.
- Edit product quantities, unit prices, and item discounts.
- Add or remove products from existing invoices.
- Modify invoice-level percentage discounts.
- Preview updated totals before saving.
- Display automatic rounding discounts.
- Cancel changes without modifying the saved invoice.
- Save changes through the backend API.
- Delete individual invoices with confirmation.

### Customer Management
- Retrieve existing customers from the API.
- Create customers directly from the invoice creation page.
- Delete customers who have no associated invoices.
- Display validation and error messages.

### Sales Reports
- View sales transactions.
- Filter transactions by date range and customer.
- Display total sales amount and invoice count.
- Open invoice details from the sales report.
- Access the delete-all-invoices feature with an explicit confirmation step.

## Technologies Used

- C#
- .NET 10
- Blazor Web App
- Interactive Server rendering
- Razor Components
- Bootstrap
- HttpClient
- Git and GitHub

## Application Pages

| Page | Route | Description |
|---|---|---|
| Home | `/` | Application landing page |
| Create Invoice | `/create-invoice` | Create invoices and manage customers |
| Invoice Details | `/invoice-details` | Search, view, edit, and delete invoices |
| Sales Reports | `/sales-reports` | View and filter sales transactions |

Invoice Details also supports opening invoices through a query parameter, such as `/invoice-details?id=16`.

## Discount Calculation

The interface supports three discount calculations:

1. **Item Discount:** A percentage applied to an individual invoice line.
2. **Invoice Discount:** A percentage applied to the subtotal after item discounts.
3. **Automatic Rounding Discount:** The remaining fractional EGP amount, removed automatically.

Example:

| Description | Amount |
|---|---:|
| Subtotal before discounts | EGP 1,300.00 |
| Item discounts | - EGP 150.00 |
| Subtotal after item discounts | EGP 1,150.00 |
| Invoice discount (5%) | - EGP 57.50 |
| Total before rounding | EGP 1,092.50 |
| Automatic rounding discount | - EGP 0.50 |
| Final invoice total | **EGP 1,092.00** |

The Blazor interface displays a live preview. The backend independently validates discounts, performs the calculations, and saves the final values.

## Project Structure

```text
SalesInvoiceUI/
├── Components/
│   ├── Layout/
│   │   ├── MainLayout.razor
│   │   └── NavMenu.razor
│   ├── Pages/
│   │   ├── Home.razor
│   │   ├── CreateInvoice.razor
│   │   ├── InvoiceDetails.razor
│   │   └── SalesReports.razor
│   ├── App.razor
│   ├── Routes.razor
│   └── _Imports.razor
├── wwwroot/
├── Program.cs
├── appsettings.json
└── SalesInvoiceUI.csproj
```

## Getting Started

### Prerequisites

- .NET 10 SDK
- SalesInvoiceAPI backend
- SQL Server configured for the backend

### Installation

1. Clone the frontend repository:

   ```bash
   git clone https://github.com/RamyBarakat01/SalesInvoiceUI.git
   ```

2. Navigate to the project directory:

   ```bash
   cd SalesInvoiceUI
   ```

3. Restore dependencies:

   ```bash
   dotnet restore
   ```

4. Start the SalesInvoiceAPI backend in a separate terminal.

5. Ensure the API base address configured for the named `SalesInvoiceAPI` HttpClient in `Program.cs` matches the backend's running address.

   During local development, the backend was configured at:

   `http://localhost:5030/`

6. Run the frontend:

   ```bash
   dotnet run
   ```

7. Open the local application in your browser.

   During development, the frontend was accessed at:

   `http://localhost:5256/`

Port numbers may differ depending on local launch settings.

## Backend Integration

The application uses `IHttpClientFactory` to create a named HTTP client called `SalesInvoiceAPI`.

Razor components send HTTP requests to the backend to retrieve customers and products, create invoices, update invoice details, manage customers, and retrieve sales reports.

The frontend does not connect directly to SQL Server. Database operations are handled by the backend through Entity Framework Core.

## Testing

The following frontend functionality has been manually tested during development:

- Creating invoices with multiple products.
- Creating and deleting customers.
- Preventing deletion of customers with existing invoices.
- Viewing invoice details.
- Editing product quantities, prices, and discounts.
- Adding and removing invoice items.
- Cancelling invoice edits.
- Deleting individual invoices.
- Viewing sales reports and applying filters.
- Applying item-level and invoice-level percentage discounts.
- Previewing automatic rounding discounts.
- Saving invoices with final whole-EGP totals.

The delete-all-invoices confirmation interface was tested, but the actual deletion of all invoice records was not executed.

## Development Status

This application has been developed and tested locally.

It requires the SalesInvoiceAPI backend and a configured SQL Server database. It has not been deployed to a public production environment.

## Related Repository

[SalesInvoiceAPI — Backend](https://github.com/RamyBarakat01/SalesInvoiceAPI)

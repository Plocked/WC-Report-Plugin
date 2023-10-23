WC Product Report Plugin - Peter Holman

My WC Product Report plugin is designed to generate a report of products sold in a specified time period in a WooCommerce store. This README provides instructions for installing and using the plugin and includes explanations of the code and my thought processes behind each section.

Installation:

Download the Plugin:
	Download the plugin from the provided ZIP file or my GitHub repository.
 
Installation via WordPress Dashboard:

 Log in to your WordPress admin dashboard.
  Navigate to Plugins > Add New.
 	Click Upload Plugin and select the downloaded ZIP file.
	Activate the plugin.
 
Usage:

  My WC Product Report plugin adds a "Product Report" submenu under the WooCommerce menu in the WordPress admin dashboard. Follow these steps to generate a product report:
  
Access the Product Report Page:
	In the WordPress admin dashboard, go to WooCommerce > Product Report.
 
Generate a Report:
	You will find a form with two date pickers (start date and end date).
 
Select the desired start and end dates.
	Click the "Generate Report" button.
 
View the Report:
 
  My plugin will validate your input and generate a report of products sold in the specified time range.
	The report includes the product name, quantity of sales, and total sales revenue for each product.
	You can also refresh the report using the AJAX refresh button.
	Export the Report as CSV:
	The report can be exported as a CSV file by clicking the "Export as CSV" button.
 
Code Explanation:

My plugin's code is organised into sections to provide specific functionality:

Main Plugin Structure:

The plugin is structured in a standard WordPress plugin format.

Admin Settings Page:

The add_admin_menu method creates an admin submenu page under WooCommerce.
The render_admin_page method displays the report generation form.

Database Query:
The process_report_generation method processes the form submission.
It validates input, performs a database query to fetch product sales data using WooCommerce functions or WPDB, and generates the report.

AJAX Functionality:
The add_ajax script method adds JavaScript to enable AJAX functionality for refreshing the report.

CSV Export (Optional):
The plugin includes an option to export the report as a CSV file.

WooCommerce Hooks:
The display_product_sales_in_order method demonstrates how to display product sales information in the order details page.

Security and Error Handling
The plugin includes security measures to prevent SQL injection and Cross-Site Scripting (XSS). Only admin users can access the report generation page.
Error handling is implemented to catch and display user-friendly error messages for issues like invalid date input.

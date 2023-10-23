<?php
/*
Plugin Name: WC-Product-Report
Description: Generates a report of products sold in a given time period.
Author: Peter Holman
*/

class WC_Product_Report {
    public function __construct() {
        // Add hooks and actions
        add_action('admin_menu', array($this, 'add_admin_menu'));
        add_action('admin_enqueue_scripts', array($this, 'enqueue_admin_scripts'));
        add_action('admin_post_generate_product_report', array($this, 'process_report_generation'));
        add_action('admin_footer', array($this, 'add_ajax_script'));
        add_action('woocommerce_admin_order_data_after_billing_address', array($this, 'display_product_sales_in_order'));
    }

    // Create the admin menu page
    public function add_admin_menu() {
        add_submenu_page(
            'woocommerce',
            'Product Report',
            'Product Report',
            'manage_options',
            'wc-product-report',
            array($this, 'render_admin_page')
        );
    }

    // I've added this to enqueue necessary scripts for the admin page
    public function enqueue_admin_scripts() {
        if (isset($_GET['page']) && $_GET['page'] === 'wc-product-report') {
            wp_enqueue_script('jquery');
            wp_enqueue_script('jquery-ui-datepicker');
        }
    }

    // Render the admin page content
    public function render_admin_page() {
        // Check user capability
        if (!current_user_can('manage_options')) {
            wp_die(__('You do not have permission to access this page.'));
        }

        // Display the form
        echo '<div class="wrap">';
        echo '<h2>Product Report</h2>';

        // Add date pickers and "Generate Report" button
        echo '<form method="post" action="' . admin_url('admin-post.php') . '">';
        echo '<label for="start_date">Start Date:</label>';
        echo '<input type="text" id="start_date" name="start_date" class="datepicker" required><br>';
        echo '<label for="end_date">End Date:</label>';
        echo '<input type="text" id="end_date" name="end_date" class="datepicker" required><br>';
        echo '<input type="submit" name="generate_report" value="Generate Report">';
        echo '<input type="hidden" name="action" value="generate_product_report">';
        echo '</form>';

        echo '<div id="product-report-results">';
        // I've added as a placeholder - display the report here
        echo '</div>';

        echo '</div>';
    }

    // Process report generation on form submission
    public function process_report_generation() {
        // Check user capability
        if (!current_user_can('manage_options')) {
            wp_die(__('You do not have permission to access this page.'));
        }

        // Validate input, fetch and display the report
        if (isset($_POST['generate_report'])) {
            // Sanitize and validate dates
            $start_date = sanitize_text_field($_POST['start_date']);
            $end_date = sanitize_text_field($_POST['end_date']);

            // Perform database query to get product sales data
            global $wpdb;
    
            // Generate the report as an array
            $report_data = array();

            // Output the report data as HTML
            echo '<table>';
            echo '<tr><th>Product Name</th><th>Quantity Sold</th><th>Total Sales Revenue</th></tr>';
            foreach ($report_data as $row) {
                echo '<tr>';
                echo '<td>' . esc_html($row['product_name']) . '</td>';
                echo '<td>' . esc_html($row['quantity_sold']) . '</td>';
                echo '<td>' . esc_html($row['total_sales_revenue']) . '</td>';
                echo '</tr>';
            }
            echo '</table>';
            exit;
        }
    }

    // AJAX functionality
    public function add_ajax_script() {
        if (isset($_GET['page']) && $_GET['page'] === 'wc-product-report') {
            ?>
            <script type="text/javascript">
                jQuery(document).ready(function ($) {
                    $('.datepicker').datepicker();

                    $('#product-report-results').on('click', '.ajax-refresh', function () {
                        $.ajax({
                            type: 'POST',
                            url: ajaxurl,
                            data: {
                                action: 'refresh_product_report',
                            },
                            success: function (response) {
                                $('#product-report-results').html(response);
                            }
                        });
                    });
                });
            </script>
            <?php
        }
    }

    // Display product sales in WooCommerce order details
    public function display_product_sales_in_order($order) {
        $order_id = $order->get_id();
    }
}

// Initialise the plugin
new WC_Product_Report();

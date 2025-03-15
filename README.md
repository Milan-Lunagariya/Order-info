# Order-info
This Page in displayed the all orders of the Users . . .


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Order Management</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" />
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" />
  <style>
    body {
      background-color: #f8f9fa;
    }
    .order-table thead {
      background-color: #343a40;
      color: white;
    }
    .status-badge {
      padding: 0.3em 0.6em;
      border-radius: 12px;
      font-size: 0.8em;
    }
    .status-pending {
      background-color: #ffc107;
      color: black;
    }
    .status-shipped {
      background-color: #0dcaf0;
    }
    .status-delivered {
      background-color: #198754;
    }
    .status-cancelled {
      background-color: #dc3545;
    }
  </style>
</head>
<body>
  <div class="container mt-5">
    <h2 class="mb-4 text-center">Order Management</h2>

    <!-- Filter -->
    <div class="d-flex justify-content-between align-items-center mb-3">
      <div>
        <label for="statusFilter" class="form-label me-2">Filter by Status:</label>
        <select id="statusFilter" class="form-select d-inline w-auto">
          <option value="all">All</option>
          <option value="pending">Pending</option>
          <option value="shipped">Shipped</option>
          <option value="delivered">Delivered</option>
          <option value="cancelled">Cancelled</option>
        </select>
      </div>
      <button class="btn btn-primary" id="addOrderBtn"><i class="fa fa-plus"></i> Add Order</button>
    </div>

    <!-- Orders Table -->
    <div class="table-responsive">
      <table class="table table-bordered order-table">
        <thead>
          <tr>
            <th>Order ID</th>
            <th>Customer</th>
            <th>Date</th>
            <th>Total</th>
            <th>Status</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody id="orderTableBody">
          <!-- Sample Orders -->
          <tr data-status="pending">
            <td>#1001</td>
            <td>Milan Lunagariya</td>
            <td>2025-03-15</td>
            <td>$200.00</td>
            <td><span class="status-badge status-pending">Pending</span></td>
            <td>
              <button class="btn btn-info btn-sm viewBtn"><i class="fa fa-eye"></i></button>
              <button class="btn btn-danger btn-sm deleteBtn"><i class="fa fa-trash"></i></button>
            </td>
          </tr>
          <tr data-status="delivered">
            <td>#1002</td>
            <td>John Doe</td>
            <td>2025-03-10</td>
            <td>$99.99</td>
            <td><span class="status-badge status-delivered">Delivered</span></td>
            <td>
              <button class="btn btn-info btn-sm viewBtn"><i class="fa fa-eye"></i></button>
              <button class="btn btn-danger btn-sm deleteBtn"><i class="fa fa-trash"></i></button>
            </td>
          </tr>
          <!-- Add more orders dynamically -->
        </tbody>
      </table>
    </div>
  </div>

  <!-- Bootstrap JS and jQuery -->
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

  <script>
    // Filter by status
    $('#statusFilter').on('change', function () {
      let selectedStatus = $(this).val();
      $('#orderTableBody tr').each(function () {
        let rowStatus = $(this).data('status');
        if (selectedStatus === 'all' || rowStatus === selectedStatus) {
          $(this).show();
        } else {
          $(this).hide();
        }
      });
    });

    // Delete confirmation
    $(document).on('click', '.deleteBtn', function () {
      if (confirm('Are you sure you want to delete this order?')) {
        $(this).closest('tr').remove();
      }
    });

    // View action (for now just alert)
    $(document).on('click', '.viewBtn', function () {
      let orderId = $(this).closest('tr').find('td:first').text();
      alert('Viewing details for Order ' + orderId);
    });

    // Add new order (mock)
    $('#addOrderBtn').on('click', function () {
      let newRow = `
        <tr data-status="pending">
          <td>#1003</td>
          <td>New Customer</td>
          <td>2025-03-15</td>
          <td>$150.00</td>
          <td><span class="status-badge status-pending">Pending</span></td>
          <td>
            <button class="btn btn-info btn-sm viewBtn"><i class="fa fa-eye"></i></button>
            <button class="btn btn-danger btn-sm deleteBtn"><i class="fa fa-trash"></i></button>
          </td>
        </tr>`;
      $('#orderTableBody').append(newRow);
    });
  </script>
</body>
</html>

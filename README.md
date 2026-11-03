# Pharma_management-
for pharma management system
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Quantapharm - Pharmacy Management System</title>
  <style>
    /* Basic styling for 1st year college project */
    body {
      font-family: Arial, sans-serif;
      background-color: #f0f4f8;
      margin: 0;
      padding: 20px;
    }

    .container {
      max-width: 950px;
      margin: 0 auto;
      background-color: #ffffff;
      padding: 25px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }

    /* Header */
    header {
      text-align: center;
      border-bottom: 2px solid #008080;
      padding-bottom: 15px;
      margin-bottom: 20px;
    }

    header h1 {
      color: #008080;
      margin: 0;
    }

    header p {
      color: #666;
      margin-top: 5px;
    }

    /* Summary Dashboard Cards */
    .dashboard-cards {
      display: flex;
      justify-content: space-between;
      gap: 15px;
      margin-bottom: 25px;
    }

    .card {
      flex: 1;
      background-color: #e6f2f2;
      border: 1px solid #b2d8d8;
      border-radius: 6px;
      padding: 15px;
      text-align: center;
    }

    .card h3 {
      margin: 0;
      font-size: 16px;
      color: #333;
    }

    .card p {
      font-size: 24px;
      font-weight: bold;
      color: #008080;
      margin: 10px 0 0 0;
    }

    /* Form Section */
    .form-section {
      background-color: #f9f9f9;
      padding: 15px;
      border: 1px solid #ddd;
      border-radius: 6px;
      margin-bottom: 25px;
    }

    .form-section h2 {
      margin-top: 0;
      font-size: 18px;
      color: #333;
    }

    .form-row {
      display: flex;
      gap: 15px;
      margin-bottom: 10px;
    }

    .form-group {
      flex: 1;
      display: flex;
      flex-direction: column;
    }

    .form-group label {
      font-size: 13px;
      margin-bottom: 5px;
      font-weight: bold;
      color: #444;
    }

    .form-group input, 
    .form-group select {
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: 14px;
    }

    button.btn-add {
      background-color: #b41772;
      color: rgb(37, 17, 195);
      border: none;
      padding: 10px 20px;
      font-size: 14px;
      border-radius: 4px;
      cursor: pointer;
      font-weight: bold;
    }

    button.btn-add:hover {
      background-color: #9ebb27;
    }

    /* Search Bar */
    .search-box {
      margin-bottom: 15px;
    }

    .search-box input {
      width: 100%;
      box-sizing: border-box;
      padding: 9px;
      font-size: 14px;
      border: 1px solid #08ac75;
      border-radius: 4px;
    }

    /* Inventory Table */
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
    }

    table th, table td {
      border: 1px solid #3726b9;
      padding: 10px;
      text-align: left;
      font-size: 14px;
    }

    table th {
      background-color: #abd1a4;
      color: rgb(110, 165, 191);
    }

    table tr:nth-child(even) {
      background-color: #f9f9f9;
    }

    table tr:hover {
      background-color: #f1f1f1;
    }

    /* Status Labels */
    .badge-in-stock {
      color: green;
      font-weight: bold;
    }

    .badge-low-stock {
      color: orange;
      font-weight: bold;
    }

    .badge-out-of-stock {
      color: red;
      font-weight: bold;
    }

    /* Action Buttons in Table */
    .btn-sell {
      background-color: #2196f3;
      color: white;
      border: none;
      padding: 5px 10px;
      border-radius: 3px;
      cursor: pointer;
      margin-right: 5px;
    }

    .btn-sell:hover {
      background-color: #0b7dda;
    }

    .btn-delete {
      background-color: #f44336;
      color: white;
      border: none;
      padding: 5px 10px;
      border-radius: 3px;
      cursor: pointer;
    }

    .btn-delete:hover {
      background-color: #da190b;
    }

    footer {
      text-align: center;
      margin-top: 25px;
      font-size: 12px;
      color: #e587d5;
    }
  </style>
</head>
<body>

  <div class="container">
    <!-- Header -->
    <header>
      <h1>Quantapharm</h1>
      <p>Pharmacy Management System - Project Dashboard</p>
    </header>

    <!-- Top Summary Cards -->
    <div class="dashboard-cards">
      <div class="card">
        <h3>Total Medicines</h3>
        <p id="totalMedicines">0</p>
      </div>
      <div class="card">
        <h3>Total Stock Count</h3>
        <p id="totalStock">0</p>
      </div>
      <div class="card">
        <h3>Low Stock Warnings</h3>
        <p id="lowStockCount">0</p>
      </div>
      <div class="card">
        <h3>Total Sales Revenue</h3>
        <p id="totalRevenue">$0.00</p>
      </div>
    </div>

    <!-- Add New Medicine Form -->
    <div class="form-section">
      <h2>Add New Medicine</h2>
      <form id="medicineForm" onsubmit="addMedicine(event)">
        <div class="form-row">
          <div class="form-group">
            <label for="medName">Medicine Name:</label>
            <input type="text" id="medName" placeholder="e.g. Paracetamol" required>
          </div>
          <div class="form-group">
            <label for="medCategory">Category:</label>
            <select id="medCategory" required>
              <option value="Pain Relief">Pain Relief</option>
              <option value="Antibiotics">Antibiotics</option>
              <option value="Vitamins">Vitamins</option>
              <option value="Diabetes">Diabetes</option>
              <option value="Syrup / Liquid">Syrup / Liquid</option>
            </select>
          </div>
        </div>

        <div class="form-row">
          <div class="form-group">
            <label for="medQuantity">Quantity in Stock:</label>
            <input type="number" id="medQuantity" min="1" placeholder="e.g. 50" required>
          </div>
          <div class="form-group">
            <label for="medPrice">Price per Unit ($):</label>
            <input type="number" id="medPrice" step="0.01" min="0.1" placeholder="e.g. 4.50" required>
          </div>
        </div>

        <button type="submit" class="btn-add">+ Add to Inventory</button>
      </form>
    </div>

    <!-- Search Section -->
    <div class="search-box">
      <input type="text" id="searchBar" onkeyup="searchMedicine()" placeholder="Search medicine by name or category...">
    </div>

    <!-- Medicine Inventory Table -->
    <h2>Current Medicine Inventory</h2>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Medicine Name</th>
          <th>Category</th>
          <th>Stock Qty</th>
          <th>Price ($)</th>
          <th>Status</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody id="inventoryTableBody">
        <!-- Rows will be added dynamically by JavaScript -->
      </tbody>
    </table>

    <footer>
      <p>&copy; Quantapharm Pharmacy Management System - College Project</p>
    </footer>
  </div>

  <!-- Basic JavaScript -->
  <script>
    // Initial sample list of medicines (Array of Objects)
    let medicines = [
      { id: 101, name: "Paracetamol 500mg", category: "Pain Relief", quantity: 45, price: 2.50 },
      { id: 102, name: "Amoxicillin 250mg", category: "Antibiotics", quantity: 6, price: 8.00 },
      { id: 103, name: "Vitamin C Chewable", category: "Vitamins", quantity: 20, price: 4.00 },
      { id: 104, name: "Cough Syrup 100ml", category: "Syrup / Liquid", quantity: 0, price: 6.50 },
      { id: 105, name: "Metformin 500mg", category: "Diabetes", quantity: 8, price: 5.20 }
    ];

    // Variable to track total money made from sales
    let totalSalesRevenue = 0;

    // Function to display medicines in the HTML table
    function displayMedicines(list) {
      let tableBody = document.getElementById("inventoryTableBody");
      tableBody.innerHTML = ""; // Clear existing table rows

      if (list.length === 0) {
        tableBody.innerHTML = "<tr><td colspan='7' style='text-align: center; color: gray;'>No medicines found!</td></tr>";
        return;
      }

      for (let i = 0; i < list.length; i++) {
        let med = list[i];
        
        // Check stock status
        let statusHtml = "";
        if (med.quantity === 0) {
          statusHtml = "<span class='badge-out-of-stock'>Out of Stock</span>";
        } else if (med.quantity <= 10) {
          statusHtml = "<span class='badge-low-stock'>Low Stock (" + med.quantity + ")</span>";
        } else {
          statusHtml = "<span class='badge-in-stock'>Available</span>";
        }

        // Create table row
        let row = "<tr>" +
          "<td>" + med.id + "</td>" +
          "<td><strong>" + med.name + "</strong></td>" +
          "<td>" + med.category + "</td>" +
          "<td>" + med.quantity + "</td>" +
          "<td>$" + med.price.toFixed(2) + "</td>" +
          "<td>" + statusHtml + "</td>" +
          "<td>" +
            "<button class='btn-sell' onclick='sellMedicine(" + med.id + ")'>Sell 1</button>" +
            "<button class='btn-delete' onclick='deleteMedicine(" + med.id + ")'>Delete</button>" +
          "</td>" +
        "</tr>";

        tableBody.innerHTML += row;
      }

      // Update the dashboard cards
      updateDashboardCounts();
    }

    // Function to calculate and update dashboard counters
    function updateDashboardCounts() {
      let totalStock = 0;
      let lowStockCount = 0;

      for (let i = 0; i < medicines.length; i++) {
        totalStock += medicines[i].quantity;
        if (medicines[i].quantity <= 10) {
          lowStockCount++;
        }
      }

      document.getElementById("totalMedicines").innerText = medicines.length;
      document.getElementById("totalStock").innerText = totalStock;
      document.getElementById("lowStockCount").innerText = lowStockCount;
      document.getElementById("totalRevenue").innerText = "$" + totalSalesRevenue.toFixed(2);
    }

    // Function to add a new medicine from form input
    function addMedicine(event) {
      event.preventDefault(); // Stop page from refreshing on form submit

      let name = document.getElementById("medName").value;
      let category = document.getElementById("medCategory").value;
      let quantity = parseInt(document.getElementById("medQuantity").value);
      let price = parseFloat(document.getElementById("medPrice").value);

      // Generate a simple next ID
      let newId = 101 + medicines.length;

      // Create new medicine object
      let newMedicine = {
        id: newId,
        name: name,
        category: category,
        quantity: quantity,
        price: price
      };

      // Add to array
      medicines.push(newMedicine);

      // Refresh table display
      displayMedicines(medicines);

      // Reset form fields
      document.getElementById("medicineForm").reset();
      alert("Success: " + name + " added to Quantapharm inventory!");
    }

    // Function to sell 1 quantity of a medicine
    function sellMedicine(id) {
      for (let i = 0; i < medicines.length; i++) {
        if (medicines[i].id === id) {
          if (medicines[i].quantity > 0) {
            medicines[i].quantity -= 1;
            totalSalesRevenue += medicines[i].price;
            alert("Sold 1 unit of " + medicines[i].name + " for $" + medicines[i].price.toFixed(2));
          } else {
            alert("Error: " + medicines[i].name + " is OUT OF STOCK!");
          }
          break;
        }
      }
      displayMedicines(medicines);
    }

    // Function to delete a medicine by ID
    function deleteMedicine(id) {
      let confirmDelete = confirm("Are you sure you want to delete this medicine?");
      if (confirmDelete) {
        medicines = medicines.filter(function(med) {
          return med.id !== id;
        });
        displayMedicines(medicines);
      }
    }

    // Function to search medicine by typing in search bar
    function searchMedicine() {
      let query = document.getElementById("searchBar").value.toLowerCase();
      let filtered = medicines.filter(function(med) {
        return med.name.toLowerCase().includes(query) || 
               med.category.toLowerCase().includes(query);
      });
      displayMedicines(filtered);
    }

    // Run this function when the page loads
    window.onload = function() {
      displayMedicines(medicines);
    };
  </script>

</body>
</html>>

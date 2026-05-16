<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Monthly Expense Tracker</title>

  <style>
    *{
      margin:0;
      padding:0;
      box-sizing:border-box;
      font-family: Arial, sans-serif;
    }

    body{
      background:#f4f4f4;
      padding:30px;
    }

    .container{
      max-width:800px;
      margin:auto;
      background:white;
      padding:25px;
      border-radius:10px;
      box-shadow:0 0 10px rgba(0,0,0,0.1);
    }

    h1{
      text-align:center;
      margin-bottom:20px;
      color:#333;
    }

    .form-group{
      margin-bottom:15px;
    }

    label{
      display:block;
      margin-bottom:5px;
      font-weight:bold;
    }

    input{
      width:100%;
      padding:10px;
      border:1px solid #ccc;
      border-radius:5px;
    }

    button{
      width:100%;
      padding:12px;
      background:#007bff;
      color:white;
      border:none;
      border-radius:5px;
      font-size:16px;
      cursor:pointer;
    }

    button:hover{
      background:#0056b3;
    }

    table{
      width:100%;
      margin-top:25px;
      border-collapse:collapse;
    }

    table th,
    table td{
      border:1px solid #ddd;
      padding:10px;
      text-align:center;
    }

    table th{
      background:#007bff;
      color:white;
    }

    .total{
      margin-top:20px;
      font-size:20px;
      font-weight:bold;
      text-align:right;
      color:#222;
    }

    .delete-btn{
      background:red;
      padding:5px 10px;
      border:none;
      color:white;
      border-radius:4px;
      cursor:pointer;
    }

    .delete-btn:hover{
      background:darkred;
    }
  </style>
</head>

<body>

  <div class="container">
    <h1>Monthly Expense Tracker</h1>

    <div class="form-group">
      <label>Date</label>
      <input type="date" id="date">
    </div>

    <div class="form-group">
      <label>Category</label>
      <input type="text" id="category" placeholder="Food, Travel, Shopping">
    </div>

    <div class="form-group">
      <label>Description</label>
      <input type="text" id="description" placeholder="Enter details">
    </div>

    <div class="form-group">
      <label>Amount (₹)</label>
      <input type="number" id="amount" placeholder="Enter amount">
    </div>

    <button onclick="addExpense()">Add Expense</button>

    <table>
      <thead>
        <tr>
          <th>Date</th>
          <th>Category</th>
          <th>Description</th>
          <th>Amount</th>
          <th>Action</th>
        </tr>
      </thead>

      <tbody id="expense-list">
      </tbody>
    </table>

    <div class="total">
      Total: ₹<span id="total">0</span>
    </div>
  </div>

  <script>
    let total = 0;

    function addExpense() {

      const date = document.getElementById("date").value;
      const category = document.getElementById("category").value;
      const description = document.getElementById("description").value;
      const amount = document.getElementById("amount").value;

      if(date === "" || category === "" || description === "" || amount === ""){
        alert("Please fill all fields");
        return;
      }

      const table = document.getElementById("expense-list");

      const row = document.createElement("tr");

      row.innerHTML = `
        <td>${date}</td>
        <td>${category}</td>
        <td>${description}</td>
        <td>₹${amount}</td>
        <td>
          <button class="delete-btn" onclick="deleteExpense(this, ${amount})">
            Delete
          </button>
        </td>
      `;

      table.appendChild(row);

      total += Number(amount);
      document.getElementById("total").innerText = total;

      document.getElementById("date").value = "";
      document.getElementById("category").value = "";
      document.getElementById("description").value = "";
      document.getElementById("amount").value = "";
    }

    function deleteExpense(button, amount) {
      button.parentElement.parentElement.remove();

      total -= Number(amount);
      document.getElementById("total").innerText = total;
    }
  </script>

</body>
</html>

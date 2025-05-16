<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
<title>Pharmacy Management System</title>
<style>
  /* Reset and base */
  * {
    box-sizing: border-box;
  }
  body {
    margin:0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: #f5f7fa;
    color: #333;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    overflow: hidden;
  }
  header {
    background: #007bff;
    color: white;
    padding: 1rem;
    text-align: center;
    font-weight: 700;
    font-size: 1.5rem;
    user-select:none;
    position: relative;
  }
  #logout-btn {
    position: absolute;
    right: 15px;
    top: 50%;
    transform: translateY(-50%);
    background: #dc3545;
    border: none;
    color: white;
    font-weight: 700;
    padding: 5px 12px;
    border-radius: 6px;
    cursor: pointer;
    display: none;
  }
  #logout-btn:hover {
    background: #b02a37;
  }
  main {
    flex: 1;
    display: flex;
    max-height: 600px;
    margin: 0 auto;
    width: 100%;
    max-width: 400px;
    background: white;
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    border-radius: 8px;
    overflow: hidden;
  }
  nav {
    width: 110px;
    background: #343a40;
    color: white;
    display: flex;
    flex-direction: column;
    padding: 0;
  }
  nav button {
    background: none;
    border: none;
    border-bottom: 1px solid #495057;
    color: white;
    padding: 12px 10px;
    font-size: 0.9rem;
    text-align: left;
    cursor: pointer;
    transition: background 0.3s;
    outline-offset: -3px;
  }
  nav button:hover, nav button.active {
    background: #007bff;
  }
  section.content-area {
    flex: 1;
    padding: 15px 20px;
    overflow-y: auto;
  }
  h2 {
    margin-top: 0;
    font-weight: 700;
    margin-bottom: 10px;
    color: #007bff;
  }
  /* Form styling */
  form {
    display: flex;
    flex-direction: column;
  }
  label {
    margin-bottom: 5px;
    font-size: 0.9rem;
    margin-top: 10px;
  }
  input[type=text], input[type=number], input[type=password], textarea {
    padding: 8px;
    font-size: 0.9rem;
    border: 1.5px solid #ccc;
    border-radius: 5px;
    transition: border-color 0.3s;
  }
  input[type=text]:focus, input[type=number]:focus, input[type=password]:focus, textarea:focus {
    border-color: #007bff;
    outline: none;
  }
  textarea {
    resize: vertical;
    min-height: 45px;
  }
  button.primary {
    background: #007bff;
    border: none;
    color: white;
    padding: 10px;
    margin-top: 20px;
    border-radius: 6px;
    font-weight: 700;
    cursor: pointer;
    transition: background 0.3s;
    user-select:none;
  }
  button.primary:hover {
    background: #0056b3;
  }
  /* Table styling */
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 10px;
    font-size: 0.9rem;
  }
  table thead {
    background: #007bff;
    color: white;
  }
  table th, table td {
    padding: 8px 6px;
    text-align: left;
    border-bottom: 1px solid #ddd;
  }
  table tbody tr:hover {
    background: #e9f3ff;
  }
  /* Search input */
  input.search-input {
    width: 100%;
    padding: 8px;
    font-size: 0.9rem;
    border-radius: 5px;
    border: 1.5px solid #ccc;
    margin-bottom: 10px;
  }
  input.search-input:focus {
    border-color: #007bff;
    outline: none;
  }
  /* Responsive adjustments */
  @media(max-width: 400px) {
    main {
      max-width: 100vw;
      border-radius: 0;
      box-shadow: none;
      height: 100vh;
      max-height: none;
    }
    nav {
      width: 80px;
      font-size: 0.8rem;
    }
    nav button {
      padding: 10px 6px;
      font-size: 0.8rem;
    }
  }
  /* Sales section styles */
  .sales-cart {
    max-height: 200px;
    overflow-y: auto;
    border: 1.5px solid #ccc;
    border-radius: 6px;
    margin-top: 10px;
  }
  .sales-cart table tbody tr td {
    padding: 6px 4px;
  }
  .cart-total {
    font-weight: 700;
    margin-top: 10px;
    text-align: right;
    font-size: 1.1rem;
    color: #007bff;
  }
  .btn-remove {
    background: #dc3545;
    border: none;
    border-radius: 4px;
    color: white;
    padding: 3px 6px;
    cursor: pointer;
    font-size: 0.8rem;
  }
  .btn-remove:hover {
    background: #b02a37;
  }
  /* Login page */
  #login-page {
    background: white;
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    border-radius: 8px;
    max-width: 400px;
    width: 100%;
    margin: 10vh auto;
    padding: 30px 25px;
  }
  #login-page h2 {
    color: #007bff;
    margin-bottom: 20px;
    text-align: center;
  }
  #login-error {
    color: #dc3545;
    margin-top: 10px;
    text-align: center;
    display: none;
  }
  /* Hide main content initially */
  #app-container {
    display: none;
    flex-direction: column;
    flex: 1;
  }
  /* Buttons below login form */
  .login-extra-buttons {
    display: flex;
    justify-content: space-between;
    margin-top: 1rem;
    font-size: 0.9rem;
  }
  .login-extra-buttons button {
    background: none;
    border: none;
    color: #007bff;
    cursor: pointer;
    padding: 0;
    user-select:none;
    font-weight: 600;
  }
  .login-extra-buttons button:hover {
    text-decoration: underline;
  }
  /* Signup and forgot-password forms */
  .hidden-form {
    display: none;
  }
</style>
</head>
<body>
<header>
  Pharmacy Management System
  <button id="logout-btn" aria-label="Logout">Logout</button>
</header>

<!-- Login page -->
<div id="login-page" role="main" aria-labelledby="login-title">
  <!-- Login form -->
  <div id="login-form-container">
    <h2 id="login-title">Pharmacy Management Login</h2>
    <form id="login-form" aria-describedby="login-error">
      <label for="login-username">Username</label>
      <input id="login-username" name="username" type="text" required autocomplete="username" placeholder="Enter username" />
      <label for="login-password">Password</label>
      <input id="login-password" name="password" type="password" required autocomplete="current-password" placeholder="Enter password" />
      <button type="submit" class="primary" aria-label="Login">Login</button>
      <p id="login-error" role="alert">Invalid username or password.</p>
    </form>
    <div class="login-extra-buttons">
      <button id="show-signup-btn" type="button">Sign Up</button>
      <button id="show-forgot-btn" type="button">Forgot Password?</button>
    </div>
  </div>

  <!-- Signup form -->
  <div id="signup-form-container" class="hidden-form" aria-hidden="true">
    <h2>Sign Up</h2>
    <form id="signup-form" aria-describedby="signup-error">
      <label for="signup-username">Username</label>
      <input id="signup-username" name="username" type="text" required autocomplete="username" placeholder="Choose a username" />
      <label for="signup-password">Password</label>
      <input id="signup-password" name="password" type="password" required autocomplete="new-password" placeholder="Choose a password" />
      <label for="signup-password-confirm">Confirm Password</label>
      <input id="signup-password-confirm" name="password-confirm" type="password" required autocomplete="new-password" placeholder="Confirm password" />
      <button type="submit" class="primary">Sign Up</button>
    </form>
    <p id="signup-error" role="alert" style="color:#dc3545; display:none; margin-top:10px; text-align:center;"></p>
    <div class="login-extra-buttons">
      <button id="back-to-login-from-signup" type="button">Back to Login</button>
    </div>
  </div>

  <!-- Forgot password form -->
  <div id="forgot-form-container" class="hidden-form" aria-hidden="true">
    <h2>Forgot Password</h2>
    <form id="forgot-form" aria-describedby="forgot-message">
      <label for="forgot-username">Username</label>
      <input id="forgot-username" name="username" type="text" required autocomplete="username" placeholder="Enter your username" />
      <button type="submit" class="primary">Retrieve Password</button>
    </form>
    <p id="forgot-message" role="alert" style="margin-top:10px; text-align:center;"></p>
    <div class="login-extra-buttons">
      <button id="back-to-login-from-forgot" type="button">Back to Login</button>
    </div>
  </div>
</div>

<!-- Main app container (hidden until login) -->
<div id="app-container">
  <main>
    <nav aria-label="Primary Navigation">
      <button id="tab-list" class="active" aria-selected="true" aria-controls="medicines-section" role="tab" tabindex="0">Medicines</button>
      <button id="tab-add" aria-selected="false" aria-controls="add-section" role="tab" tabindex="-1">Add</button>
      <button id="tab-stock" aria-selected="false" aria-controls="stock-section" role="tab" tabindex="-1">Stock</button>
      <button id="tab-search" aria-selected="false" aria-controls="search-section" role="tab" tabindex="-1">Search</button>
      <button id="tab-sales" aria-selected="false" aria-controls="sales-section" role="tab" tabindex="-1">Sales</button>
    </nav>
    <section class="content-area" tabindex="0">
      <!-- Medicines List Section -->
      <section id="medicines-section" role="tabpanel" aria-labelledby="tab-list">
        <h2>Medicine List</h2>
        <table aria-label="Medicine List Table">
          <thead>
            <tr><th>Name</th><th>Price</th><th>Quantity</th></tr>
          </thead>
          <tbody id="medicine-list-table-body">
          </tbody>
        </table>
        <p id="medicine-list-empty" style="text-align:center; margin-top:10px; color:#666; display:none;">No medicines added yet.</p>
      </section>
      <!-- Add Medicine Section -->
      <section id="add-section" role="tabpanel" aria-labelledby="tab-add" hidden>
        <h2>Add New Medicine</h2>
        <form id="add-medicine-form" aria-label="Add New Medicine Form">
          <label for="med-name">Name<span aria-hidden="true" style="color:red;">*</span></label>
          <input id="med-name" name="name" type="text" required autocomplete="off" placeholder="Medicine name" />
          <label for="med-desc">Description</label>
          <textarea id="med-desc" name="description" placeholder="Brief description (optional)"></textarea>
          <label for="med-price">Price (per unit)<span aria-hidden="true" style="color:red;">*</span></label>
          <input id="med-price" name="price" type="number" min="0" step="0.01" required placeholder="e.g. 4.99" />
          <label for="med-qty">Initial Quantity<span aria-hidden="true" style="color:red;">*</span></label>
          <input id="med-qty" name="quantity" type="number" min="0" step="1" required placeholder="e.g. 10" />
          <button type="submit" class="primary" aria-label="Add Medicine">Add Medicine</button>
        </form>
      </section>
      <!-- Manage Stock Section -->
      <section id="stock-section" role="tabpanel" aria-labelledby="tab-stock" hidden>
        <h2>Manage Stock</h2>
        <form id="update-stock-form" aria-label="Update Stock Form">
          <label for="stock-medicine-select">Select Medicine<span aria-hidden="true" style="color:red;">*</span></label>
          <select id="stock-medicine-select" required aria-required="true" aria-describedby="stock-qty-label">
          </select>
          <label id="stock-qty-label" for="stock-qty">Adjust Quantity (can be negative)<span aria-hidden="true" style="color:red;">*</span></label>
          <input type="number" id="stock-qty" name="stock-change" required step="1" value="0" />
          <button type="submit" class="primary" aria-label="Update Stock">Update Stock</button>
        </form>
      </section>
      <!-- Search Section -->
      <section id="search-section" role="tabpanel" aria-labelledby="tab-search" hidden>
        <h2>Search Medicine</h2>
        <input type="text" id="search-input" class="search-input" placeholder="Search by name or description" aria-label="Search Medicines" autocomplete="off" />
        <table aria-label="Search Results" id="search-results-table" style="display:none;">
          <thead>
            <tr><th>Name</th><th>Price</th><th>Quantity</th></tr>
          </thead>
          <tbody id="search-results-body">
          </tbody>
        </table>
        <p id="search-no-results" style="text-align:center; margin-top:10px; color:#666; display:none;">No matching medicines found.</p>
      </section>
      <!-- Sales Section -->
      <section id="sales-section" role="tabpanel" aria-labelledby="tab-sales" hidden>
        <h2>Sales Management</h2>
        <form id="add-to-cart-form" aria-label="Add Medicine to Cart Form">
          <label for="sales-medicine-select">Select Medicine<span aria-hidden="true" style="color:red;">*</span></label>
          <select id="sales-medicine-select" required aria-required="true">
          </select>
          <label for="sales-qty">Quantity to Sell<span aria-hidden="true" style="color:red;">*</span></label>
          <input type="number" id="sales-qty" name="sales-qty" required min="1" step="1" value="1" />
          <button type="submit" class="primary" aria-label="Add to Cart">Add to Cart</button>
        </form>
        <div class="sales-cart" aria-live="polite" aria-label="Cart items">
          <table aria-label="Cart table">
            <thead>
              <tr><th>Name</th><th>Qty</th><th>Price</th><th>Total</th><th>Action</th></tr>
            </thead>
            <tbody id="cart-body">
            </tbody>
          </table>
        </div>
        <p class="cart-total" id="cart-total">Total: $0.00</p>
        <button id="btn-clear-cart" class="primary" style="background:#dc3545; margin-top:10px;">Clear Cart</button>
        <button id="btn-checkout" class="primary" style="margin-top:10px;">Checkout</button>
      </section>
    </section>
  </main>
</div>
<script>
  // Pharmacy Management System Script

  // Data structure to hold medicines, users and localStorage keys
  const STORAGE_KEY = 'pharmacy_medicines';
  const LOGIN_STATE_KEY = 'pharmacy_loggedin';
  const USERS_KEY = 'pharmacy_users';

  let medicines = [];
  let cart = [];

  // Default demo user
  const DEMO_USER = { username: 'admin', password: 'password123' };

  // Utility function to format number as currency
  function formatCurrency(num) {
    return '$' + num.toFixed(2);
  }

  // Load medicines from localStorage or initialize empty with sample data
  function loadMedicines() {
    const stored = localStorage.getItem(STORAGE_KEY);
    if (stored) {
      medicines = JSON.parse(stored);
    } else {
      // Sample initial medicines data
      medicines = [
        {name: 'Paracetamol', description: 'Pain reliever and fever reducer', price: 1.50, quantity: 120},
        {name: 'Amoxicillin', description: 'Antibiotic for bacterial infections', price: 3.75, quantity: 50},
        {name: 'Aspirin', description: 'Pain reliever, blood thinner', price: 1.00, quantity: 80},
        {name: 'Cough Syrup', description: 'Relieves cough and throat irritation', price: 4.20, quantity: 30},
        {name: 'Vitamin C', description: 'Dietary supplement', price: 2.25, quantity: 150}
      ];
      saveMedicines();
    }
  }
  // Save current medicines to localStorage
  function saveMedicines() {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(medicines));
  }

  // Load users from localStorage or initialize with default user
  function loadUsers() {
    const stored = localStorage.getItem(USERS_KEY);
    if (stored) {
      return JSON.parse(stored);
    } else {
      const initialUsers = [DEMO_USER];
      localStorage.setItem(USERS_KEY, JSON.stringify(initialUsers));
      return initialUsers;
    }
  }
  // Save users to localStorage
  function saveUsers(users) {
    localStorage.setItem(USERS_KEY, JSON.stringify(users));
  }

  // Find user by username
  function findUser(username) {
    const users = loadUsers();
    return users.find(u => u.username.toLowerCase() === username.toLowerCase());
  }

  // Render medicines list table
  function renderMedicineList() {
    const tbody = document.getElementById('medicine-list-table-body');
    const emptyMsg = document.getElementById('medicine-list-empty');
    tbody.innerHTML = '';
    if (medicines.length === 0) {
      emptyMsg.style.display = 'block';
      return;
    } else {
      emptyMsg.style.display = 'none';
    }
    medicines.forEach(med => {
      const tr = document.createElement('tr');
      tr.innerHTML = `<td>${med.name}</td><td>${formatCurrency(med.price)}</td><td>${med.quantity}</td>`;
      tbody.appendChild(tr);
    });
  }

  // Fill select options for stock management and sales
  function fillSelectOptions() {
    const stockSelect = document.getElementById('stock-medicine-select');
    const salesSelect = document.getElementById('sales-medicine-select');

    [stockSelect, salesSelect].forEach(select => {
      select.innerHTML = '';
      medicines.forEach(med => {
        let option = document.createElement('option');
        option.value = med.name;
        option.textContent = med.name;
        select.appendChild(option);
      });
      if (select.options.length === 0) {
        let option = document.createElement('option');
        option.textContent = 'No medicines available';
        option.disabled = true;
        select.appendChild(option);
      }
    });
  }

  // Add new medicine from form input
  function addMedicine(e) {
    e.preventDefault();
    const nameInput = document.getElementById('med-name');
    const descInput = document.getElementById('med-desc');
    const priceInput = document.getElementById('med-price');
    const qtyInput = document.getElementById('med-qty');

    let name = nameInput.value.trim();
    let description = descInput.value.trim();
    let price = parseFloat(priceInput.value);
    let quantity = parseInt(qtyInput.value);

    if (!name || isNaN(price) || price < 0 || isNaN(quantity) || quantity < 0) {
      alert('Please enter valid medicine details.');
      return;
    }

    // Check if medicine with this name exists (case-insensitive)
    if (medicines.some(m => m.name.toLowerCase() === name.toLowerCase())) {
      alert('Medicine with this name already exists.');
      return;
    }

    medicines.push({name, description, price, quantity});
    saveMedicines();
    renderMedicineList();
    fillSelectOptions();

    // Clear form
    nameInput.value = '';
    descInput.value = '';
    priceInput.value = '';
    qtyInput.value = '';
    alert('Medicine added successfully!');
  }

  // Update stock quantity
  function updateStock(e) {
    e.preventDefault();
    const select = document.getElementById('stock-medicine-select');
    const qtyChangeInput = document.getElementById('stock-qty');

    const name = select.value;
    const change = parseInt(qtyChangeInput.value);

    if (!name || isNaN(change)) {
      alert('Please select a medicine and enter a valid quantity change.');
      return;
    }

    let med = medicines.find(m => m.name === name);
    if (!med) {
      alert('Medicine not found.');
      return;
    }

    let newQty = med.quantity + change;
    if (newQty < 0) {
      alert('Resulting quantity cannot be negative.');
      return;
    }
    med.quantity = newQty;
    saveMedicines();
    renderMedicineList();
    fillSelectOptions();
    qtyChangeInput.value = '0';
    alert('Stock updated successfully!');
  }

  // Render search results
  function renderSearchResults(results) {
    const tbody = document.getElementById('search-results-body');
    const table = document.getElementById('search-results-table');
    const noResults = document.getElementById('search-no-results');

    tbody.innerHTML = '';
    if (results.length === 0) {
      table.style.display = 'none';
      noResults.style.display = 'block';
      return;
    }

    noResults.style.display = 'none';
    table.style.display = 'table';

    results.forEach(med => {
      const tr = document.createElement('tr');
      tr.innerHTML = `<td>${med.name}</td><td>${formatCurrency(med.price)}</td><td>${med.quantity}</td>`;
      tbody.appendChild(tr);
    });
  }

  // Handle search input
  function handleSearchInput(e) {
    const query = e.target.value.trim().toLowerCase();
    if (!query) {
      renderSearchResults([]);
      return;
    }
    const results = medicines.filter(med => 
      med.name.toLowerCase().includes(query) || (med.description && med.description.toLowerCase().includes(query))
    );
    renderSearchResults(results);
  }

  // Cart and sales management

  // Render cart table
  function renderCart() {
    const tbody = document.getElementById('cart-body');
    tbody.innerHTML = '';
    if (cart.length === 0) {
      tbody.innerHTML = '<tr><td colspan="5" style="text-align:center;color:#666;">Cart is empty</td></tr>';
      document.getElementById('cart-total').textContent = 'Total: $0.00';
      return;
    }
    let total = 0;
    cart.forEach((item, index) => {
      let itemTotal = item.price * item.quantity;
      total += itemTotal;
      const tr = document.createElement('tr');

      // Remove button element
      const btnRemove = `<button class="btn-remove" aria-label="Remove ${item.name} from cart" data-index="${index}">×</button>`;

      tr.innerHTML = `
        <td>${item.name}</td>
        <td>${item.quantity}</td>
        <td>${formatCurrency(item.price)}</td>
        <td>${formatCurrency(itemTotal)}</td>
        <td>${btnRemove}</td>
      `;
      tbody.appendChild(tr);
    });
    document.getElementById('cart-total').textContent = `Total: ${formatCurrency(total)}`;
  }

  // Add to cart
  function addToCart(e) {
    e.preventDefault();
    const select = document.getElementById('sales-medicine-select');
    const qtyInput = document.getElementById('sales-qty');

    const name = select.value;
    const qty = parseInt(qtyInput.value);

    if (!name || isNaN(qty) || qty < 1) {
      alert('Please select medicine and enter valid quantity.');
      return;
    }

    const med = medicines.find(m => m.name === name);
    if (!med) {
      alert('Medicine not found.');
      return;
    }

    if (med.quantity < qty) {
      alert(`Not enough stock! Available quantity: ${med.quantity}`);
      return;
    }

    // Check if in cart already
    let cartItem = cart.find(c => c.name === name);
    if (cartItem) {
      if (cartItem.quantity + qty > med.quantity) {
        alert(`Cannot add ${qty} more. Only ${med.quantity - cartItem.quantity} available.`);
        return;
      }
      cartItem.quantity += qty;
    } else {
      cart.push({name: med.name, price: med.price, quantity: qty});
    }
    renderCart();
  }

  // Remove from cart by index
  function removeFromCart(index) {
    if (index >= 0 && index < cart.length) {
      cart.splice(index, 1);
      renderCart();
    }
  }

  // Clear cart
  function clearCart() {
    if (confirm('Clear the entire cart?')) {
      cart = [];
      renderCart();
    }
  }

  // Checkout - reduce stock and clear cart
  function checkout() {
    if (cart.length === 0) {
      alert('Cart is empty.');
      return;
    }
    // Check stock again before confirming
    for (let item of cart) {
      const med = medicines.find(m => m.name === item.name);
      if (!med || med.quantity < item.quantity) {
        alert(`Stock updated! Not enough quantity of ${item.name}. Please adjust your cart.`);
        return;
      }
    }
    // Reduce stock quantity
    for (let item of cart) {
      const med = medicines.find(m => m.name === item.name);
      med.quantity -= item.quantity;
    }
    saveMedicines();
    alert('Checkout successful! Stock updated.');
    cart = [];
    renderCart();
    renderMedicineList();
    fillSelectOptions();
  }

  // Navigation tabs switching
  function switchTab(e) {
    const buttons = document.querySelectorAll('nav button');
    buttons.forEach(btn => {
      btn.classList.remove('active');
      btn.setAttribute('aria-selected', 'false');
      btn.setAttribute('tabindex', '-1');
    });
    e.target.classList.add('active');
    e.target.setAttribute('aria-selected', 'true');
    e.target.setAttribute('tabindex', '0');

    const tabId = e.target.id;
    const sections = document.querySelectorAll('section[role="tabpanel"]');
    sections.forEach(sec => {
      sec.hidden = true;
      sec.setAttribute('tabindex','-1');
    });

    let showSection;
    switch (tabId) {
      case 'tab-list': showSection = 'medicines-section'; break;
      case 'tab-add': showSection = 'add-section'; break;
      case 'tab-stock': showSection = 'stock-section'; break;
      case 'tab-search': showSection = 'search-section'; break;
      case 'tab-sales': showSection = 'sales-section'; break;
    }

    const sectionToShow = document.getElementById(showSection);
    if (sectionToShow) {
      sectionToShow.hidden = false;
      sectionToShow.setAttribute('tabindex','0');
      sectionToShow.focus();
    }
  }

  // Handle login
  function handleLogin(e) {
    e.preventDefault();
    const usernameInput = document.getElementById('login-username');
    const passwordInput = document.getElementById('login-password');
    const errorMsg = document.getElementById('login-error');

    const username = usernameInput.value.trim();
    const password = passwordInput.value.trim();

    const user = findUser(username);
    if (user && user.password === password) {
      // Set login state
      localStorage.setItem(LOGIN_STATE_KEY, 'true');
      showApp();
      errorMsg.style.display = 'none';
      // Clear login fields
      usernameInput.value = '';
      passwordInput.value = '';
    } else {
      errorMsg.style.display = 'block';
    }
  }

  // Handle sign up
  function handleSignup(e) {
    e.preventDefault();
    const usernameInput = document.getElementById('signup-username');
    const passwordInput = document.getElementById('signup-password');
    const passwordConfirmInput = document.getElementById('signup-password-confirm');
    const errorMsg = document.getElementById('signup-error');

    const username = usernameInput.value.trim();
    const password = passwordInput.value;
    const passwordConfirm = passwordConfirmInput.value;

    if (username.length < 3) {
      errorMsg.textContent = 'Username must be at least 3 characters.';
      errorMsg.style.display = 'block';
      return;
    }
    if (password.length < 6) {
      errorMsg.textContent = 'Password must be at least 6 characters.';
      errorMsg.style.display = 'block';
      return;
    }
    if (password !== passwordConfirm) {
      errorMsg.textContent = 'Passwords do not match.';
      errorMsg.style.display = 'block';
      return;
    }

    if (findUser(username)) {
      errorMsg.textContent = 'Username already exists.';
      errorMsg.style.display = 'block';
      return;
    }

    // Add new user
    const users = loadUsers();
    users.push({username, password});
    saveUsers(users);

    alert('Sign up successful! You can now log in.');

    // Reset fields and switch back to login
    usernameInput.value = '';
    passwordInput.value = '';
    passwordConfirmInput.value = '';
    errorMsg.style.display = 'none';
    showLoginForm();
  }

  // Handle forgot password
  function handleForgot(e) {
    e.preventDefault();
    const usernameInput = document.getElementById('forgot-username');
    const messageP = document.getElementById('forgot-message');

    const username = usernameInput.value.trim();
    if (!username) {
      messageP.textContent = 'Please enter your username.';
      messageP.style.color = '#dc3545';
      return;
    }

    const user = findUser(username);
    if (user) {
      // For demo only: reveal password
      messageP.style.color = '#007bff';
      messageP.textContent = `Password for "${user.username}" is: ${user.password}`;
    } else {
      messageP.style.color = '#dc3545';
      messageP.textContent = 'Username not found.';
    }
  }

  // Show/hide login, signup, forgot password forms
  function showLoginForm() {
    document.getElementById('login-form-container').style.display = 'block';
    document.getElementById('signup-form-container').style.display = 'none';
    document.getElementById('forgot-form-container').style.display = 'none';

    document.getElementById('login-error').style.display = 'none';
    document.getElementById('signup-error').style.display = 'none';
    document.getElementById('forgot-message').textContent = '';

    document.getElementById('signup-form-container').setAttribute('aria-hidden', 'true');
    document.getElementById('forgot-form-container').setAttribute('aria-hidden', 'true');
    document.getElementById('login-form-container').removeAttribute('aria-hidden');
  }
  function showSignupForm() {
    document.getElementById('login-form-container').style.display = 'none';
    document.getElementById('signup-form-container').style.display = 'block';
    document.getElementById('forgot-form-container').style.display = 'none';

    document.getElementById('signup-error').style.display = 'none';

    document.getElementById('signup-form-container').removeAttribute('aria-hidden');
    document.getElementById('forgot-form-container').setAttribute('aria-hidden', 'true');
    document.getElementById('login-form-container').setAttribute('aria-hidden', 'true');
  }
  function showForgotForm() {
    document.getElementById('login-form-container').style.display = 'none';
    document.getElementById('signup-form-container').style.display = 'none';
    document.getElementById('forgot-form-container').style.display = 'block';

    document.getElementById('forgot-message').textContent = '';

    document.getElementById('forgot-form-container').removeAttribute('aria-hidden');
    document.getElementById('signup-form-container').setAttribute('aria-hidden', 'true');
    document.getElementById('login-form-container').setAttribute('aria-hidden', 'true');
  }

  // Show app and hide login
  function showApp() {
    document.getElementById('login-page').style.display = 'none';
    document.getElementById('app-container').style.display = 'flex';
    document.getElementById('logout-btn').style.display = 'block';
  }

  // Hide app and show login
  function showLogin() {
    document.getElementById('login-page').style.display = 'block';
    document.getElementById('app-container').style.display = 'none';
    document.getElementById('logout-btn').style.display = 'none';
    showLoginForm();
  }

  // Logout function
  function logout() {
    if (confirm('Are you sure you want to logout?')) {
      localStorage.removeItem(LOGIN_STATE_KEY);
      cart = [];
      showLogin();
    }
  }

  // On load
  document.addEventListener('DOMContentLoaded', () => {
    // Check if user logged in
    let loggedIn = localStorage.getItem(LOGIN_STATE_KEY) === 'true';

    if (loggedIn) {
      loadMedicines();
      renderMedicineList();
      fillSelectOptions();
      renderCart();
      showApp();
    } else {
      showLogin();
    }

    // Form events
    document.getElementById('login-form').addEventListener('submit', handleLogin);
    document.getElementById('signup-form').addEventListener('submit', handleSignup);
    document.getElementById('forgot-form').addEventListener('submit', handleForgot);

    // Navigation between login, signup, forgot forms
    document.getElementById('show-signup-btn').addEventListener('click', showSignupForm);
    document.getElementById('show-forgot-btn').addEventListener('click', showForgotForm);
    document.getElementById('back-to-login-from-signup').addEventListener('click', showLoginForm);
    document.getElementById('back-to-login-from-forgot').addEventListener('click', showLoginForm);

    document.getElementById('add-medicine-form').addEventListener('submit', addMedicine);
    document.getElementById('update-stock-form').addEventListener('submit', updateStock);
    document.getElementById('search-input').addEventListener('input', handleSearchInput);
    document.getElementById('add-to-cart-form').addEventListener('submit', addToCart);

    document.getElementById('logout-btn').addEventListener('click', logout);

    // Cart remove buttons (event delegation)
    document.getElementById('cart-body').addEventListener('click', e => {
      if (e.target.classList.contains('btn-remove')) {
        const index = parseInt(e.target.dataset.index);
        removeFromCart(index);
      }
    });
    // Clear and Checkout buttons
    document.getElementById('btn-clear-cart').addEventListener('click', clearCart);
    document.getElementById('btn-checkout').addEventListener('click', checkout);

    // Nav buttons
    const navButtons = document.querySelectorAll('nav button');
    navButtons.forEach(btn => {
      btn.addEventListener('click', switchTab);
      btn.addEventListener('keydown', e => {
        if (e.key === 'ArrowDown' || e.key === 'ArrowRight') {
          e.preventDefault();
          let next = btn.nextElementSibling || btn.parentElement.firstElementChild;
          next.focus();
        } else if (e.key === 'ArrowUp' || e.key === 'ArrowLeft') {
          e.preventDefault();
          let prev = btn.previousElementSibling || btn.parentElement.lastElementChild;
          prev.focus();
        }
      });
    });
  });
</script>
</body>
</html>


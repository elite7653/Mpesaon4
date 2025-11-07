<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Chartered Investments</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: "Poppins", sans-serif;
    }

    body {
      height: 100vh;
      background: linear-gradient(
          rgba(0, 0, 0, 0.55),
          rgba(0, 0, 0, 0.75)
        ),
        url("https://images.unsplash.com/photo-1569025690938-a00729c9e1a9?auto=format&fit=crop&w=1600&q=80")
          no-repeat center center/cover;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      overflow: hidden;
    }

    .container {
      text-align: center;
      background: rgba(0, 0, 0, 0.65);
      padding: 40px 30px;
      border-radius: 20px;
      backdrop-filter: blur(6px);
      box-shadow: 0 0 15px rgba(255, 255, 255, 0.1);
      animation: fadeIn 2s ease-in-out;
      width: 90%;
      max-width: 500px;
    }

    .logo {
      width: 80px;
      height: 80px;
      border-radius: 50%;
      background: white;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 auto 20px;
      animation: float 3s ease-in-out infinite;
    }

    .logo span {
      font-size: 2.5rem;
      font-weight: bold;
      color: black;
    }

    .container h1 {
      font-size: 2rem;
      margin-bottom: 10px;
      color: #fff;
    }

    .container p {
      color: #ddd;
      font-size: 1rem;
      margin-bottom: 30px;
    }

    .pay-btn {
      background: #0dbf6f;
      color: white;
      border: none;
      padding: 14px 35px;
      border-radius: 30px;
      font-size: 1.1rem;
      cursor: pointer;
      transition: 0.3s;
      animation: float 3s ease-in-out infinite;
    }

    .pay-btn:hover {
      background: #0ca862;
      transform: scale(1.05);
    }

    @keyframes float {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-5px); }
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: scale(0.95); }
      to { opacity: 1; transform: scale(1); }
    }

    /* Modal styles */
    .modal {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.7);
      display: flex;
      align-items: center;
      justify-content: center;
      opacity: 0;
      visibility: hidden;
      transition: 0.3s;
      z-index: 10;
    }

    .modal.active {
      opacity: 1;
      visibility: visible;
    }

    .modal-content {
      background: white;
      color: black;
      padding: 30px;
      border-radius: 15px;
      width: 90%;
      max-width: 400px;
      text-align: center;
      animation: fadeIn 0.5s;
    }

    .modal-content input {
      width: 100%;
      padding: 10px;
      margin: 8px 0;
      border-radius: 8px;
      border: 1px solid #ccc;
      outline: none;
    }

    .confirm-btn {
      background: #0dbf6f;
      color: white;
      border: none;
      padding: 12px 25px;
      border-radius: 30px;
      cursor: pointer;
      margin-top: 10px;
      transition: 0.3s;
    }

    .confirm-btn:hover {
      background: #0ca862;
    }

    /* Success Popup */
    .success-popup {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) scale(0);
      background: white;
      color: black;
      padding: 30px;
      border-radius: 15px;
      text-align: center;
      width: 90%;
      max-width: 350px;
      transition: 0.4s;
      z-index: 20;
    }

    .success-popup.active {
      transform: translate(-50%, -50%) scale(1);
    }

    .success-popup h3 {
      color: #0dbf6f;
      margin-bottom: 10px;
    }

    .success-popup p {
      color: #333;
      margin-bottom: 20px;
    }

    .close-btn {
      background: #0dbf6f;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 25px;
      cursor: pointer;
    }

    .close-btn:hover {
      background: #0ca862;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="logo">
      <span>C</span>
    </div>
    <h1>Chartered Investments</h1>
    <p>Invest with confidence and grow your wealth the smart way.</p>
    <button class="pay-btn" onclick="openModal()">Pay Now</button>
  </div>

  <!-- Payment Modal -->
  <div class="modal" id="paymentModal">
    <div class="modal-content">
      <h3>Make Payment</h3>
      <p>Enter details below to proceed</p>
      <input type="tel" id="phone" placeholder="Enter your Mpesa number" />
      <input type="number" id="amount" placeholder="Enter amount (KES)" />
      <button class="confirm-btn" onclick="confirmPayment()">Confirm Payment</button>
    </div>
  </div>

  <!-- Success Popup -->
  <div class="success-popup" id="successPopup">
    <h3>✅ Payment Instructions Sent</h3>
    <p>Use Paybill <b>522522</b> and Account <b>2347864</b> to complete payment in your M-Pesa menu.</p>
    <button class="close-btn" onclick="closeSuccess()">Close</button>
  </div>

  <script>
    const modal = document.getElementById("paymentModal");
    const popup = document.getElementById("successPopup");

    function openModal() {
      modal.classList.add("active");
    }

    function confirmPayment() {
      const phone = document.getElementById("phone").value.trim();
      const amount = document.getElementById("amount").value.trim();

      if (!phone || !amount) {
        alert("Please enter both phone number and amount.");
        return;
      }

      // Show success popup and instructions
      modal.classList.remove("active");
      popup.classList.add("active");

      // Try to open Mpesa app (USSD)
      setTimeout(() => {
        window.location.href = "tel:*334#";
      }, 1500);

      // After showing popup, redirect to WhatsApp
      setTimeout(() => {
        window.location.href = "https://wa.me/254791892024?text=Hello%20Chartered%20Investments,%20I%20have%20completed%20my%20payment%20of%20KES%20" + amount + "%20from%20" + phone;
      }, 6000);
    }

    function closeSuccess() {
      popup.classList.remove("active");
    }
  </script>
</body>
</html>

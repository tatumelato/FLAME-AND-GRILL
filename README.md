<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DELICIOUS FLAME AND GRILL</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
      background: linear-gradient(to bottom, black, #222);
      color: gold;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
    }

    header, footer {
      text-align: center;
      padding: 20px;
    }

    main {
      width: 90%;
      max-width: 600px;
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(10px);
      border-radius: 15px;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.5);
      padding: 20px;
      margin: 20px 0;
    }

    .bank-details {
      background: rgba(0, 0, 0, 0.3);
      padding: 20px;
      border-radius: 10px;
      margin-bottom: 20px;
      border: 1px solid rgba(255, 215, 0, 0.3);
    }

    .bank-details h2 {
      text-align: center;
      margin-top: 0;
      color: gold;
    }

    .bank-details p {
      margin: 10px 0;
    }

    .bank-details strong {
      color: white;
    }

    h1 {
      margin: 0 0 20px;
      color: gold;
    }

    label {
      display: block;
      margin-bottom: 10px;
      font-weight: bold;
    }

    input, select, button {
      width: 100%;
      padding: 12px;
      margin-bottom: 15px;
      border: none;
      border-radius: 10px;
      outline: none;
      font-size: 16px;
    }

    input, select {
      background: rgba(255, 255, 255, 0.2);
      color: gold;
    }

    button {
      background: linear-gradient(to bottom, gold, #cc9900);
      color: black;
      font-weight: bold;
      cursor: pointer;
      box-shadow: 0 5px #995c00;
      transition: transform 0.2s, box-shadow 0.2s;
    }

    button:active {
      transform: translateY(2px);
      box-shadow: 0 3px #995c00;
    }

    button:hover {
      background: linear-gradient(to bottom, #cc9900, gold);
    }

    .countdown {
      font-size: 24px;
      font-weight: bold;
      margin-bottom: 20px;
      text-align: center;
      color: gold;
      background: linear-gradient(to bottom, black, gold);
      padding: 15px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5);
    }

    .confirmation-popup {
      display: none;
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 80%;
      max-width: 400px;
      background: rgba(0, 0, 0, 0.9);
      border-radius: 15px;
      padding: 20px;
      box-shadow: 0 5px 20px rgba(0, 0, 0, 0.8);
      color: gold;
      text-align: center;
      z-index: 1000;
    }

    .popup-buttons {
      display: flex;
      justify-content: space-around;
      margin-top: 20px;
    }

    .popup-buttons button {
      width: 45%;
      padding: 10px;
      font-size: 16px;
      font-weight: bold;
    }

    .popup-yes {
      background: gold;
      color: black;
    }

    .popup-no {
      background: black;
      color: gold;
      border: 2px solid gold;
    }

    .important-note {
      font-size: 14px;
      color: white;
      margin-top: 20px;
      text-align: center;
    }
  </style>
</head>
<body>
  <header>
    <h1>DELICIOUS FLAME AND GRILL</h1>
  </header>

  <main>
    <div class="countdown" id="countdown"></div>

    <div class="bank-details">
      <h2>Banking Details</h2>
      <p><strong>Bank:</strong> ABSA Bank</p>
      <p><strong>Account Name:</strong> JT Mosounyana</p>
      <p><strong>Account Number:</strong> 9311552533</p>
      <p><strong>Branch Code:</strong> 470010</p>
      <p><strong>Reference:</strong> Your Full Name</p>
      <p><strong>Account Type:</strong> Savings</p>
      <p><strong>Email Proof of Payment to:</strong> jaymosou@gmail.com</p>
    </div>

    <form id="ticketForm">
      <label for="name">Full Name:</label>
      <input type="text" id="name" name="name" placeholder="Enter your full name" required>

      <label for="email">Email:</label>
      <input type="email" id="email" name="email" placeholder="Enter your email" required>

      <label for="phone">Phone Number:</label>
      <input type="tel" id="phone" name="phone" placeholder="Enter your phone number" required>

      <label for="ticket">Ticket Type:</label>
      <select id="ticket" name="ticket" required>
        <option value="" disabled selected>Select Ticket Type</option>
        <option value="EARLY BIRD - R150">EARLY BIRD - R150</option>
        <option value="GENERAL - R250">GENERAL - R250</option>
        <option value="VIP - R800">VIP - R800</option>
      </select>

      <label for="proof">Upload Proof of Payment:</label>
      <input type="file" id="proof" name="proof" accept="image/*" required>

      <div>
        <input type="checkbox" id="terms" required>
        <label for="terms">I agree to the terms and conditions</label>
      </div>

      <button type="button" onclick="confirmSubmission()">Submit</button>
    </form>

    <p class="important-note">
      <strong>Note:</strong> Please keep your proof of purchase for verification purposes.
    </p>
  </main>

  <div class="confirmation-popup" id="confirmationPopup">
    <p>Are you sure you want to submit?</p>
    <div class="popup-buttons">
      <button class="popup-yes" onclick="submitForm()">Yes</button>
      <button class="popup-no" onclick="closePopup()">No</button>
    </div>
  </div>

  <footer>
    <p>© 2025 DELICIOUS FLAME AND GRILL. All rights reserved.</p>
  </footer>

  <script>
    // Countdown Timer
    const eventDate = new Date("2025-03-01T18:00:00").getTime();
    const countdownEl = document.getElementById("countdown");

    setInterval(() => {
      const now = new Date().getTime();
      const distance = eventDate - now;

      if (distance < 0) {
        countdownEl.innerText = "The event has started!";
        return;
      }

      const days = Math.floor(distance / (1000 * 60 * 60 * 24));
      const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
      const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
      const seconds = Math.floor((distance % (1000 * 60)) / 1000);

      countdownEl.innerText = `Event starts in: ${days}d ${hours}h ${minutes}m ${seconds}s`;
    }, 1000);

    // Confirmation Popup
    function confirmSubmission() {
      document.getElementById("confirmationPopup").style.display = "block";
    }

    function closePopup() {
      document.getElementById("confirmationPopup").style.display = "none";
    }

    function submitForm() {
      const name = document.getElementById("name").value;
      const email = document.getElementById("email").value;
      const phone = document.getElementById("phone").value;
      const ticket = document.getElementById("ticket").value;

      // WhatsApp message
      const message = `Hello, I would like to book a ticket for the DELICIOUS FLAME AND GRILL event.\n\nName: ${name}\nEmail: ${email}\nPhone: ${phone}\nTicket Type: ${ticket}\n\nProof of payment has been sent to jaymosou@gmail.com\n\nThank you.`;
      
      // Open WhatsApp
      window.location.href = `https://wa.me/27613137674?text=${encodeURIComponent(message)}`;
      
      // Close popup
      closePopup();
    }
  </script>
</body>
</html>

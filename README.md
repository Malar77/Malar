# Malar
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Banking System</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f4;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h2 {
            text-align: center;
            color: #333;
        }
        .button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
            margin: 10px 0;
        }
        .button:hover {
            background-color: #45a049;
        }
        label, p {
            margin: 10px 0;
        }
        input {
            width: 100%;
            padding: 10px;
            margin: 5px 0 20px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        #balance {
            font-size: 24px;
            font-weight: bold;
            color: #4CAF50;
        }
        #message {
            color: red;
        }
    </style>
</head>
<body>

    <div class="container">
        <h2>Simple Banking System</h2>

        <div>
            <p>Account Holder: <strong>John Doe</strong></p>
            <p>Account Number: <strong>1234567890</strong></p>
            <p>Your Current Balance: <span id="balance">$1000.00</span></p>
            <p id="message"></p>
        </div>

        <!-- Deposit Section -->
        <div>
            <h3>Deposit Money</h3>
            <label for="depositAmount">Enter Deposit Amount:</label>
            <input type="number" id="depositAmount" placeholder="Enter amount to deposit">
            <button class="button" onclick="depositMoney()">Deposit</button>
        </div>

        <!-- Withdraw Section -->
        <div>
            <h3>Withdraw Money</h3>
            <label for="withdrawAmount">Enter Withdraw Amount:</label>
            <input type="number" id="withdrawAmount" placeholder="Enter amount to withdraw">
            <button class="button" onclick="withdrawMoney()">Withdraw</button>
        </div>

        <!-- Transfer Section -->
        <div>
            <h3>Transfer Money</h3>
            <label for="transferAmount">Enter Transfer Amount:</label>
            <input type="number" id="transferAmount" placeholder="Enter amount to transfer">
            <label for="recipientAccount">Recipient Account Number:</label>
            <input type="number" id="recipientAccount" placeholder="Enter recipient account number">
            <button class="button" onclick="transferMoney()">Transfer</button>
        </div>

    </div>

    <script>
        let balance = 1000.00;

        // Function to update the displayed balance
        function updateBalance() {
            document.getElementById('balance').innerText = `$${balance.toFixed(2)}`;
        }

        // Deposit function
        function depositMoney() {
            let depositAmount = parseFloat(document.getElementById('depositAmount').value);
            if (isNaN(depositAmount) || depositAmount <= 0) {
                document.getElementById('message').innerText = 'Please enter a valid amount greater than zero.';
            } else {
                balance += depositAmount;
                document.getElementById('message').innerText = `Deposited: $${depositAmount.toFixed(2)}`;
                updateBalance();
            }
            document.getElementById('depositAmount').value = ''; // Clear input field
        }

        // Withdraw function
        function withdrawMoney() {
            let withdrawAmount = parseFloat(document.getElementById('withdrawAmount').value);
            if (isNaN(withdrawAmount) || withdrawAmount <= 0) {
                document.getElementById('message').innerText = 'Please enter a valid amount greater than zero.';
            } else if (withdrawAmount > balance) {
                document.getElementById('message').innerText = 'Insufficient funds.';
            } else {
                balance -= withdrawAmount;
                document.getElementById('message').innerText = `Withdrawn: $${withdrawAmount.toFixed(2)}`;
                updateBalance();
            }
            document.getElementById('withdrawAmount').value = ''; // Clear input field
        }

        // Transfer function
        function transferMoney() {
            let transferAmount = parseFloat(document.getElementById('transferAmount').value);
            let recipientAccount = document.getElementById('recipientAccount').value;

            if (isNaN(transferAmount) || transferAmount <= 0) {
                document.getElementById('message').innerText = 'Please enter a valid amount greater than zero.';
            } else if (transferAmount > balance) {
                document.getElementById('message').innerText = 'Insufficient funds for transfer.';
            } else if (recipientAccount === '') {
                document.getElementById('message').innerText = 'Please enter a valid recipient account number.';
            } else {
                balance -= transferAmount;
                document.getElementById('message').innerText = `Transferred: $${transferAmount.toFixed(2)} to Account ${recipientAccount}`;
                updateBalance();
            }
            document.getElementById('transferAmount').value = ''; // Clear input field
            document.getElementById('recipientAccount').value = ''; // Clear input field
        }
    </script>

</body>
</html>

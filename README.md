<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Payment Website</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            background-color: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            border-radius: 5px;
            width: 300px;
        }
        .container h1 {
            margin-top: 0;
            text-align: center;
        }
        .container form, .container .payment-methods {
            display: flex;
            flex-direction: column;
        }
        .container input, .container button {
            padding: 10px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 3px;
        }
        .container button {
            background-color: #007bff;
            color: #fff;
            cursor: pointer;
        }
        .container button:hover {
            background-color: #0056b3;
        }
        .error {
            color: red;
            text-align: center;
            margin-bottom: 10px;
        }
        .payment-info {
            text-align: center;
            font-size: 16px;
            margin-top: 20px;
        }
        .upload-receipt {
            display: none;
            flex-direction: column;
        }
    </style>
</head>
<body>
    <div class="container" id="accessContainer">
        <h1>Payment Access</h1>
        <form id="accessForm">
            <input type="text" id="fanId" placeholder="Fan ID" required>
            <input type="password" id="passcode" placeholder="Passcode" required>
            <div class="error" id="errorMessage"></div>
            <button type="submit">Access Payment Page</button>
        </form>
    </div>

    <div class="container" id="paymentContainer" style="display: none;">
        <h1>Choose Payment Method</h1>
        <div class="payment-methods">
            <button onclick="displayPaymentInfo('CashApp')">CashApp</button>
            <button onclick="displayPaymentInfo('PayPal')">PayPal</button>
            <button onclick="displayPaymentInfo('Crypto')">Crypto</button>
            <button onclick="displayPaymentInfo('Venmo')">Venmo</button>
        </div>
        <div class="payment-info" id="paymentInfo"></div>
        <div class="upload-receipt" id="uploadReceipt">
            <label for="receipt">Upload Payment Receipt:</label>
            <input type="file" id="receipt" accept="image/*, .pdf" required>
            <button onclick="validateReceipt()">Submit Receipt</button>
        </div>
        <div class="error" id="receiptError"></div>
    </div>

    <div class="container" id="confirmationContainer" style="display: none;">
        <h1>Payment Confirmation</h1>
        <p>Your payment has been successfully submitted and confirmed.</p>
    </div>

    <script>
        document.getElementById('accessForm').addEventListener('submit', function(event) {
            event.preventDefault();
            const fanId = document.getElementById('fanId').value;
            const passcode = document.getElementById('passcode').value;
            const errorMessage = document.getElementById('errorMessage');

            if (fanId === '0689256' && passcode === 'XX34Y8KV10') {
                document.getElementById('accessContainer').style.display = 'none';
                document.getElementById('paymentContainer').style.display = 'block';
            } else {
                errorMessage.textContent = 'Invalid Fan ID or Passcode. Please try again.';
            }
        });

        function displayPaymentInfo(method) {
            const paymentInfo = document.getElementById('paymentInfo');
            const uploadReceipt = document.getElementById('uploadReceipt');
            let info = '';
            switch (method) {
                case 'CashApp':
                    info = '$SoutherFusion';
                    break;
                case 'PayPal':
                    info = 'M.howe30@yahoo.com';
                    break;
                case 'Crypto':
                    info = '13CVQWXmyHA1YgcH9JDUq7BWkZGfcdKEoN';
                    break;
                case 'Venmo':
                    info = '@Matthew-Howe-238';
                    break;
                default:
                    info = '';
            }
            paymentInfo.textContent = info;
            uploadReceipt.style.display = 'flex';
        }

        function validateReceipt() {
            const receipt = document.getElementById('receipt');
            const receiptError = document.getElementById('receiptError');
            if (receipt.files.length > 0) {
                document.getElementById('paymentContainer').style.display = 'none';
                document.getElementById('confirmationContainer').style.display = 'block';
            } else {
                receiptError.textContent = 'Please upload a payment receipt before proceeding.';
            }
        }
    </script>
</body>
</html>

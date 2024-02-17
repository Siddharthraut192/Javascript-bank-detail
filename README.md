# Javascript-bank-detail
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bank account</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }

        #output {
            margin-top: 20px;
        }
    </style>
</head>
<body>      

<script>
    
    var name, address, contact, balance;
    var depositHistory = [];
    var withdrawHistory = [];

    function manageAccount() {
        
        if (!name) {
            name = prompt("Enter your name:");
            address = prompt("Enter your address:");
            contact = prompt("Enter your contact number:");
            balance = parseFloat(prompt("Enter your initial deposit:")) || 0; 
        }

    
        var output = "Name: " + name + "<br>";
        output += "Address: " + address + "<br>";
        output += "Contact: " + contact + "<br>";
        output += "Current Balance: Rs" + balance.toFixed(2) + "<br>";

        
        var action = prompt("Choose an action: \n 1. Deposit \n 2. Withdraw \n 3. Check Current Balance");

        
        switch (parseInt(action)) {
            case 1:
                var depositAmount = parseFloat(prompt("Enter the deposit amount:"));
                if (!isNaN(depositAmount)) {
                    balance += depositAmount;
                    depositHistory.push({ amount: depositAmount, balance: balance });
                    output += "Deposited: Rs" + depositAmount.toFixed(2) + "<br>";
                } else {
                    output += "Invalid deposit amount entered.<br>";
                }
                break;
            case 2:
                var withdrawAmount = parseFloat(prompt("Enter the withdrawal amount:"));
                if (!isNaN(withdrawAmount)) {
                    if (withdrawAmount <= balance) {
                        balance -= withdrawAmount;
                        withdrawHistory.push({ amount: withdrawAmount, balance: balance });
                        output += "Withdrawn: Rs" + withdrawAmount.toFixed(2) + "<br>";
                    } else {
                        output += "Insufficient funds for withdrawal.<br>";
                    }
                } else {
                    output += "Invalid withdrawal amount entered.<br>";
                }
                break;
            case 3:
            output += "Current Balance: Rs" + balance.toFixed(2) + "<br>"; 
                break;
            default:
                output += "Invalid option selected.<br>";
        }

        output += "Total Balance: Rs" + balance.toFixed(2) + "<br>";
    
        output += "<br>Deposit History:<br>";
        depositHistory.forEach(entry => {
            output += `Deposited: Rs${entry.amount.toFixed(2)}, Balance: Rs${entry.balance.toFixed(2)}<br>`;
        });

        output += "<br>Withdrawal History:<br>";
        withdrawHistory.forEach(entry => {
            output += `Withdrawn: Rs${entry.amount.toFixed(2)}, Balance: Rs${entry.balance.toFixed(2)}<br>`;
        });

    
        document.getElementById("output").innerHTML = output;
    }
</script>

<h2>Bank account</h2>
<button onclick="manageAccount()">Manage Account</button>

<div id="output"></div>

</body>
</html>

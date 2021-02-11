 # MPESA EXPRESS
 
 Mpesa Express is an open source library Designed, Developed and Maintained by Dev Thagichu [ https://github.com/devthagichu ].
 
 The Library is a wrapper around Safaricom's Daraja API that can be used in Node JS Applications
 
 Safaricom Daraja API: https://developer.safaricom.co.ke/
 
 
 ## support
 
 - [x] Typescript
 - [x] Promises
 
 
 
 ## Getting Started
![mpesa express](nodejs.png)


### Installation 

        npm install mpesa-express



### Quick Start

        npm install mpesa-express  

Add to project

        const Mpesa = require ('mpesa-express');

        Initialize  with options
 
        const options = {

         // Cousumer Key and Consumer Secret are found on your Client Dashboard
         // https://developer.safaricom.co.ke/user/me/apps

         consumer_key: "<STRING>",
         consumer_secret: "<STRING>",

         // Passkey , Business Shortcode and Shortcode are found on the Test Credentials Page
         // https://developer.safaricom.co.ke/test_credentials

         passkey: "<STRING>",
         BusinessShortCode: "<INTEGER>", // 174379
         ShortCode: "<INTEGER>", //174379

         // Secruity Credentials is generated by adding the consumer secret as 
         // the Initiator Security Password and clicking Generate Credentials
         
         SecurityCredential: "<STRING>",
         Initiator: "<STRING>",
         
         callBackBaseUrl: "<STRING>",
       };
 
    
        const mpesa = new Mpesa(options)



### Features

###   Lipa Na M-Pesa Online Payment API
###### Use this API to initiate online payment on behalf of a customer.
https://developer.safaricom.co.ke/lipa-na-m-pesa-online/apis/post/stkpush/v1/processrequest

        mpesa.sktPush(Amount, PhoneNumber, AccountReference, TransactionDesc) 

### Lipa Na M-Pesa Query Request API
###### Use this API to check the status of a Lipa Na M-Pesa Online Payment.
https://developer.safaricom.co.ke/lipa-na-m-pesa-online/apis/post/stkpushquery/v1/query

        mpesa.stkCheck(CheckoutRequestID)

### C2B Register URL
 ###### Use this API to register validation and confirmation URLs on M-Pesa 
 https://developer.safaricom.co.ke/c2b/apis/post/registerurl

        // The C2B options are found on the API Section under C2B Register URL 
        // https://developer.safaricom.co.ke/c2b/apis/post/registerurl


        // Confirmation URL is the CALLBACK URL to your app
        // Safaricom will send a POST request to this url once a C2B payment is confirmed
        
        const ConfirmationURL = "<STRING>" // https://youapp/confirm

        // Validation URL is the CALLBACK URL to your app
        // Safaricom will send a POST request to this url once a C2B payment is confirmed
        
        const ValidationURL = "<STRING>" // https://youapp/valid

        // Both ConfirmationURL and ValidationURL must be HTTPS

        // Response types are: Completed or Cancelled.
        
        const ResponseType = "<STRING>"

        // This is the Business C2B shortcode
        
        const ShortCode = "<INTEGER>" // 600000
        
        mpesa.c2bRegister( ConfirmationURL, ValidationURL, ResponseType, ShortCode)

### C2B Simulate Transaction
###### This API is used to make payment requests from Client to Business (C2B). 
###### You can use the sandbox provided test credentials down below to simulates a payment made from 
###### the client phone's STK/SIM Toolkit menu, and enables you to receive the payment requests in real time.
https://developer.safaricom.co.ke/c2b/apis/post/simulate

        // The C2B options are found on the API Section under C2B Simulate Transaction
        // https://developer.safaricom.co.ke/c2b/apis/post/simulate


        // This is the Business C2B shortcode
        
        const ShortCode = "<INTEGER>" // 600000

        // The transaction type you want to simulate
        // CommandID types are: CustomerPayBillOnline OR CustomerBuyGoodsOnline.
        
        const CommandID = "<STRING>"

        // The transaction amount you want to simulate 
        
        const Amount = "<INTEGER>" // 1

        // The Transacting Mobile Number
        
        const Msisdn = "<INTEGER>" // 2547xxxxxxxx

        // Any Refferance or ID that you would what to associate the 
        // transaction with
        
        const BillRefNumber = "<STRING>" // Invoice-001
        
        mpesa.c2bTransact(ShortCode, CommandID, Amount, Msisdn, BillRefNumber)

### B2C Payment Request
###### Use this API to transact between an M-Pesa short code to a phone number registered on M-Pesa.
https://developer.safaricom.co.ke/b2c/apis/post/paymentrequest

        mpesa.b2c(Amount, PartyA, PartyB, Remarks, CommandID, Occassion, SecurityCredential)

### Account Balance Request
###### Use this API to enquire the balance on an M-Pesa BuyGoods (Till Number)
https://developer.safaricom.co.ke/account-balance/apis/post/query

        mpesa.checkAccountBalance(CommandID, IdentifierType, Remarks)
        
## Support for this Library

All the support for this library is done through: https://github.com/devthagichu/mpesa-express/issues


## Author
Anthony Gitau Thagichu
Twitter: https://twitter.com/devthagichu



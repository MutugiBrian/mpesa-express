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

        or

        yarn add mpesa-express



Add to project

        const Mpesa = require ('mpesa-express');

        // Initialize  with options

        const options = {

         // Cousumer Key and Consumer Secret are found on your Client Dashboard
         // https://developer.safaricom.co.ke/user/me/apps

         consumer_key: "<STRING>",
         consumer_secret: "<STRING>",

         // Passkey , Business Shortcode and Shortcode are found on the Test Credentials Page
         // https://developer.safaricom.co.ke/test_credentials

         passkey: "<STRING>", // bfb279f9aa9bdbcf158e97dd71a467cd2e0c893059b10f78e6b72ada1ed2c919
         BusinessShortCode: "<INTEGER>", // 174379
         ShortCode: "<INTEGER>", //600000

         // Secruity Credentials is generated by adding the consumer secret as
         // the Initiator Security Password and clicking Generate Credentials

         SecurityCredential: "<STRING>", //Safaricom147!
         Initiator: "<STRING>", //testapi

         callBackBaseUrl: "<STRING>",
       };


        const mpesa = new Mpesa(options)

### Features

### Lipa Na M-Pesa Online Payment API

###### Use this API to initiate online payment on behalf of a customer.

https://developer.safaricom.co.ke/lipa-na-m-pesa-online/apis/post/stkpush/v1/processrequest

        // The Lipa Na M-Pesa Online Payment options are found on the API Section under Lipa Na M-Pesa Online Payment API
        // https://developer.safaricom.co.ke/lipa-na-m-pesa-online/apis/post/stkpush/v1/processrequest


        // The transaction amount you want to simulate

        const Amount = "<INTEGER>" // 1

        // The Transacting Mobile Number

        const PhoneNumber = "<INTEGER>" // 2547xxxxxxxx

        // Any Refferance or ID that you would what to associate the
        // transaction with

        const AccountReference = "<STRING>" // Invoice-001

        // Any Description that you would what to associate the
        // transaction with

        const TransactionDesc = "<STRING>" // Admission fee


        mpesa.sktPush(Amount, PhoneNumber, AccountReference, TransactionDesc)
        .then((result) => console.log(result))
        .catch((error) => console.error(error));

### Lipa Na M-Pesa Query Request API

###### Use this API to check the status of a Lipa Na M-Pesa Online Payment.

https://developer.safaricom.co.ke/lipa-na-m-pesa-online/apis/post/stkpushquery/v1/query

        // The Lipa Na M-Pesa Query Request API options are found on the API Section under Lipa Na M-Pesa Query Request API
        // https://developer.safaricom.co.ke/lipa-na-m-pesa-online/apis/post/stkpushquery/v1/query

        // This is a global unique identifier of the processed checkout transaction request.

        const CheckoutRequestID = "<STRING>" // ws_CO_DMZ_123212312_2342347678234

        mpesa.stkCheck(CheckoutRequestID)
        .then((result) => console.log(result))
        .catch((error) => console.error(error));

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
        .then((result) => console.log(result))
        .catch((error) => console.error(error));

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
        .then((result) => console.log(result))
        .catch((error) => console.error(error));

### B2C Payment Request

###### Use this API to transact between an M-Pesa short code to a phone number registered on M-Pesa.

https://developer.safaricom.co.ke/b2c/apis/post/paymentrequest

        // The B2C Payment Request options are found on the API Section under B2C Payment Request
        // https://developer.safaricom.co.ke/b2c/apis/post/paymentrequest


        // The transaction amount you want to simulate
        const Amount = "<INTEGER>" // 1

        // The B2C shortcode
        const PartyA = "<INTEGER>" // 600000

        // The Phone Number receiving the money
        const PartyB = "<INTEGER>" // 254722000000

        // 	Comments that are sent along with the transaction.
        const Remarks = "<STRING>" // Monthly check

        // The transaction type you want to simulate
        // CommandID types are:
        // SalaryPayment
        // BusinessPayment
        // PromotionPayment

        const CommandID = "<STRING>" // BusinessPayment

        // Any additional information to be associated with the transaction.

        const Occassion = "<STRING>" // Payment for ...

        // Secruity Credentials is generated by adding the consumer secret as the Initiator Security
        // Password and clicking Generate Credentials

        const SecurityCredential = "<STRING>" // 32SzVdmCvjpmQfw3X2RK8UAv7xuhh304dXxFC5+3lslkk2TDJY/Lh6ESVwtqMxJzF7qA==

        mpesa.b2c(Amount, PartyA, PartyB, Remarks, CommandID, Occassion, SecurityCredential)
        .then((result) => console.log(result))
        .catch((error) => console.error(error));

### Account Balance Request

###### Use this API to enquire the balance on an M-Pesa BuyGoods (Till Number)

https://developer.safaricom.co.ke/account-balance/apis/post/query

        // The Account Balance Request options are found on the API Section under Account Balance Request
        // https://developer.safaricom.co.ke/account-balance/apis/post/query


        // Type of commands

        const CommandID = "<STRING>" // AccountBalance

        // Type of organization receiving the transaction
        // Types examples
        // 1 – MSISDN
        // 2 – Till Number
        // 4 – Organization short code

        const IdentifierType = "<INTEGER>" // 1

        // 	Comments that are sent along with the transaction.

        const Remarks = "<STRING>" // Monthly check

        mpesa.checkAccountBalance(CommandID, IdentifierType, Remarks)
        .then((result) => console.log(result))
        .catch((error) => console.error(error));
        
### Test Details

        Shortcode 1:   600147
        Initiator Name:   (Shortcode 1)        testapi
        Security Credential:   (Shortcode 1)   Safaricom147!
        Shortcode 2:   600000
        Test MSISDN:   254708374149
        ExpiryDate:   2017-11-13T18:59:13+03:00
        Lipa Na Mpesa Online Shortcode:   174379
        Lipa Na Mpesa Online PassKey:    bfb279f9aa9bdbcf158e97dd71a467cd2e0c893059b10f78e6b72ada1ed2c919
        

## Support for this Library

All the support for this library is done through: https://github.com/devthagichu/mpesa-express/issues

## Author Details

Anthony Gitau Thagichu

Twitter: https://twitter.com/devthagichu

Facebook: https://www.facebook.com/devthagichu

Youtube: https://www.youtube.com/channel/UC7_SdKhua8Ysxzj2y_1km3Q?view_as=subscriber

Linkedn: https://www.linkedin.com/in/devthagichu/

## License

This project is licensed under the MIT License.

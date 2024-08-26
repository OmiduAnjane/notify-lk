Notify.LK Documentation
---------------------

*   [Introduction](#introduction)
*   [Installation](#installation)
*   [Usage](#usage)
*   [API Reference](#api-reference)
*   [Examples](#examples)
*   [Author](#author)
*   [License](#license)

Introduction
------------

Welcome to the NotifyLK NPM package documentation. This package enables you to send SMS messages, check account status, and manage contacts using the Notify.lk API.

Installation
------------

```sh
npm install notify-lk --save
```

Run the above command in your project directory to install the package.

Usage
-----

Here’s how to use the NotifyLK package in your Node.js application:

```ts 
const NotifyLK = require('notify-lk');
    
const notify = new NotifyLK('YOUR_USER_ID', 'YOUR_API_KEY', 'YOUR_SENDER_ID');
    
notify.sendSMS('9471XXXXXXX', 'Hello from NotifyLK')
        .then(response => console.log(response))
        .catch(error => console.error(error));
```

API Reference
-------------

### NotifyLK(userId, apiKey, senderId)

Constructor for creating a new instance of the NotifyLK class.

*   **userId:** _string_ - Your Notify.lk user ID.
*   **apiKey:** _string_ - Your Notify.lk API key.
*   **senderId:** _string_ - The sender ID for your messages (default: NotifyDEMO).

### sendSMS(to, message, options)

Sends an SMS to the specified number.

*   **to:** _string_ - The recipient's phone number in 94XXXXXXXXX format.
*   **message:** _string_ - The message to be sent.
*   **options:** _object_ - Additional options for the message (optional).

### getAccountStatus()

Retrieves the account status including the balance and active status.

### saveContact(to, options)

Saves a contact in your Notify.lk account.

### getSMSHistory(limit)

Retrieves the SMS history with an optional limit on the number of records.

### addContact(contact, options)

Adds a new contact to your Notify.lk account. Useful for managing your contact list.

*   **contact:** _object_ - The contact details to add. Includes `name` and `phone` properties.
*   **options:** _object_ - Additional options for adding the contact (optional).

Examples
--------

### 1\. Sending a Simple SMS

This example demonstrates how to send a simple SMS using the NotifyLK package:
```ts
const NotifyLK = require('notify-lk');
    
const notify = new NotifyLK('YOUR_USER_ID', 'YOUR_API_KEY', 'YOUR_SENDER_ID');
    
notify.sendSMS('9471XXXXXXX', 'Hello from NotifyLK')
    .then(response => console.log('SMS Sent:', response))
    .catch(error => console.error('Error Sending SMS:', error));
```
### 2\. Checking Account Status

This example shows how to check your account's status, including balance and active status:
```ts
notify.getAccountStatus()
    .then(status => console.log('Account Status:', status))
    .catch(error => console.error('Error Fetching Account Status:', error));
```
### 3\. Saving a New Contact

You can save a new contact in your Notify.lk account with additional details:
```ts
notify.saveContact('9471XXXXXXX', {
    contact_fname: 'John',
    contact_lname: 'Doe',
    contact_email: 'john.doe@example.com',
    contact_address: '123 Example St, City, Country'
})
  .then(response => console.log('Contact Saved:', response))
  .catch(error => console.error('Error Saving Contact:', error));
```
### 4\. Sending SMS with Unicode Characters

To send an SMS containing Unicode characters (e.g., emojis, non-Latin scripts), include the `type` option:
```ts
notify.sendSMS('9471XXXXXXX', 'Hello from NotifyLK 😊', { type: 'unicode' })
    .then(response => console.log('Unicode SMS Sent:', response))
    .catch(error => console.error('Error Sending Unicode SMS:', error));
```
### 5\. Retrieving SMS History

This example retrieves the last 10 SMS messages sent using your account:
```ts
notify.getSMSHistory(10)
    .then(history => console.log('SMS History:', history))
    .catch(error => console.error('Error Fetching SMS History:', error));
```
### 6\. Bulk SMS Sending

Sending SMS to multiple recipients in a loop:
```ts
const numbers = ['9471XXXXXXX', '9472XXXXXXX', '9473XXXXXXX'];
const message = 'Hello from NotifyLK';
    
numbers.forEach(number => {
    notify.sendSMS(number, message)
        .then(response => console.log(`SMS Sent to ${number}:`, response))
        .catch(error => console.error(`Error Sending SMS to ${number}:`, error));
    });
```
### 7\. Handling SMS Errors Gracefully

This example demonstrates how to handle errors, such as invalid phone numbers or API issues:
```ts
notify.sendSMS('invalid_number', 'This message will fail')
    .then(response => console.log('SMS Sent:', response))
    .catch(error => {
        if (error.response && error.response.data) {
            console.error('API Error:', error.response.data);
        } else {
            console.error('Unknown Error:', error.message);
        }
    });
```
### 8\. Scheduling SMS for Future Delivery

If Notify.lk supports scheduling (hypothetical, as the real API may not), you could do something like this:
```ts
const scheduleDate = new Date(Date.now() + 60 * 60 * 1000); // 1 hour from now
notify.sendSMS('9471XXXXXXX', 'This message is scheduled for future delivery', { send_at: scheduleDate.toISOString() })
    .then(response => console.log('Scheduled SMS Sent:', response))
    .catch(error => console.error('Error Scheduling SMS:', error));
```
Author
------

This package is maintained by **Omindu Dissanayake**.

For more information, visit the [GitHub profile](https://github.com/OmiduAnjane).
License
-------

This package is licensed under the MIT License. See the LICENSE file for more information.
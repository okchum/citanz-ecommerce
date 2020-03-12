# CITANZ SilverStripe eCommerce
No doc at this stage - use on your own risk.
## How does it work?
It doesn't...

## Email Configuration
```
SilverStripe\Control\Email\Email:
  noreply_email:
    noreply@yourdomainname.com: 'Sitename'
```

## Cronjob
set up a cronjob to purge pending carts (on a daily basis)

## Product
`Cita\eCommerce\Model\Product`


## Order
`Cita\eCommerce\Model\Order`
### implement `createInvoiceRows` function in extension to create your own invoice rows

### turn off order's default buttons:
```
Cita\eCommerce\Model\Order:
  default_buttons:
    send_invoice    :   true
    cheque_cleared  :   true
    refund          :   true
    send_tracking   :   true
    debit_cleared   :   true
```

## OrderItem

### Email sending
If you want to customise emails, please implement below methods:
- SendCustomerEmail($from, $to, $str, $customer_sent_flag)
- SendAdminEmail($from, $to_admin, $str, $admin_sent_flag)

and make sure you update the 'sent' prop in $customer_sent_flag & $admin_sent_flag to `true`

## Checkout values
### GST
GST calculation is based on the subtotal amount AFTER the discount (is there is one) plus shipping cost.

### Shipping cost
- Shipping cost IS NOT included in GST calculation
- Shipping cost DOES NOT accept discount (if you want to give the freight provider money, you extend the classes and customise the calculation and take manage your own calculation from there.)


## FAQ
### Test cards?
#### POLi
Username: DemoShopper
Password: DemoShopper

#### Payment Express
Card: 4111111111111111
Card Holder: YOUR_NAME
Expiry: [leave it as it is]
CVV: 100

#### Paystation
Card: 5555555555554444
Card Holder: YOUR_NAME
Expiry: 0521
CVV: 100

### Why Payment Express method rounds my payable total (or amount shows up on the payment gateway is different from what's on the checkout grand total)?
When on sandbox mode, Payment Express only allows integer value to be the amount to pay, therefore we have to round the amount before we pass it to Payment Express's payment gateway.
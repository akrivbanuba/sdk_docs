# Token Management

To use our SDK in your project, you need to have an SDK token. The FAQ below explains our token management process and guides you on how to store and update tokens after its expiration. Please, read all the information carefully.

### What is an SDK token?

SDK token is an automatically generated set of characters unique to each client sent in .txt format. It activates the licenced SDK functionality in the client app. There are two types of tokes:

* Demo token is provided to start the SDK trial. It's valid for 14 days, our standard trial period. The token activates all SDK features for you to assess the SDK performance in your project.
* Commercial token is provided after you make payment. It’s valid throughout the prepaid period. The token activates the SDK features defined by your software licence.

:::note Once the token expires, the Banuba watermark and screen blur will appear automatically in your app. :::

Therefore, please:

* Don’t use demo tokens in live apps.
* Observe payments of your SDK licence and renew the commercial token on time.

### Why do we use tokens?

The SDK token system helps us to manage billing, prevent our software from frauds, inappropriate and unconditioned usage that violates the SDK licencing terms.

### How do I get one?

* To get the demo token and start the SDK trial, please contact your sales manager or send us a request via the website form.
* The commercial token is generated and sent out by your account manager who guides your project within our company.

### How does it work?

**Activation**

Together with the token, you will receive a configuration file config.json which contains the required SDK resources defined by the token.

**Token storage**

We recommend storing your token on the server as it drastically facilitates the process of token renewal.

:::caution If you store the token in the app, you need to upload its newest version to the App Store or Play Market after you renew the token. :::

**Expiry and renewal**

Tokens are valid only throughout the predefined period of time. If the token expiration does not exceed one month, you can use SDK in your app with Banuba watermark. If the token expiration **exceeds one month**, you won't be able to use the SDK in your app, but the app will continue to work without it. There will not be a possibility to renew the current token. You'll need to generate a new one. See the explanation of token expiration below:

| Token expired?  | What happens with Face AR SDK    |
| --------------- | -------------------------------- |
| No              | Works as expected                |
| Yes, <= 1 month | Works but watermark is displayed |
| Yes, > 1 month  | Functionality won't work         |

To restore the access, you need to request a new token and renew it in your app.

* **Demo tokens** may be renewed per client’s request in case the client hasn’t enough time to evaluate the SDK.
* **Commercial tokens** are renewed by an account manager only after the client’s pre-payment for an agreed period.

**Other questions left?**

Please, read all the information carefully and feel free to contact us if you have more questions.

# script connecting to the nodemailer with Oauth 
---
Steps
- [x] Create Project [Google Developer Console](https://console.cloud.google.com/home/dashboard)
- [x] Go to the API Credentials & create OAuth consent screen
- [x] Click Credentials then Create Credentials then Click OAuth ClientID
- [x] Click web application and add Authorized redirect URIs 
`https://developers.google.com/oauthplayground`
 to this link then will you get client_id and client_secret go to the above link 
 - [x] click on the checkbox and put client_id and client_secret **Use your own OAuth credentials** then 
 - [x] On the **Select & authorize APIs** write this link `https://mail.google.com` click the Authorized api button, it will redirect you to access to your Gmail account then i will give me warning about your app is not verify ignore it 
---
## dependencies
npm i nodemailer googleapis dotenv
---
***secrets this should be come from dotenv file***
```js
const CLIENT_ID = process.env.CLIENT_ID;
const CLEINT_SECRET = process.env.CLIENT_SECRET;
const REDIRECT_URI = 'https://developers.google.com/oauthplayground';
const REFRESH_TOKEN = process.env.REFRESH_TOKEN;

const oAuth2Client = new google.auth.OAuth2(
  CLIENT_ID,
  CLEINT_SECRET,
  REDIRECT_URI
);
oAuth2Client.setCredentials({ refresh_token: REFRESH_TOKEN });

```

***Function***
```js
async function sendMail() {
  try {
    const accessToken = await oAuth2Client.getAccessToken();

    const transport = nodemailer.createTransport({
      service: 'gmail',
      auth: {
        type: 'OAuth2',
        user: 'example@gmail.com',
        clientId: CLIENT_ID,
        clientSecret: CLEINT_SECRET,
        refreshToken: REFRESH_TOKEN,
        accessToken: accessToken,
      },
    });
    const mailOptions = {
      from: '<example@gmail.com>',
      to: '<example@gmail.com',
      subject: 'Hello from gmail using API',
      text: 'Hello from gmail email using API',
      html: '<h1>Hello from gmail email using API</h1>',
    };

    const result = await transport.sendMail(mailOptions);
    return result;
  } catch (error) {
    return error;
  }
}

sendMail()
  .then((result) => console.log('Email sent...', result))
  .catch((error) => console.log(error.message));
```

:smile: Contact :point_right: [Fiverr](https://www.fiverr.com/dvlopermohsin?up_rollout=true) :point_right: [LinkedIn](https://www.linkedin.com/in/mohsin-ali-soomro/) :point_right: [Facebook](https://web.facebook.com/profile.php?id=100004936470736) :point_right: WhatsApp :heavy_plus_sign: :nine: :three: :one: :one: :three: :four: :zero: :three: :zero: :seven: :eight:

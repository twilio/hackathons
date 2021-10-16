![cover pic](static/hackathon-how-to.png)

## Table of Contents
* [Why does Twilio sponsor hackathons](README.md#why-does-twilio-sponsor-hackathons)
* [TODO before the hackathon](README.md#TODO-before-the-hackathon)
* [TODO after the hackathon](README.md#TODO-after-the-hackathon)
* [Quick-and-easy code snippets](README.md#quick-and-easy-code-snippets)
* [Tutorials](README.md#tutorials)
    * [Tutorials by product](README.md#by-product)
    * [Tutorials by language](README.md#by-language)
        * [Node.js Tutorials](README.md#nodejs)
        * [React.js Tutorials](README.md#nodejs)
        * [Python Tutorials](README.md#python)
        * [Swift Tutorials](README.md#swift)
        * [Java Tutorials](README.md#java)
    * [YouTube videos](README.md#youtube-videos)
* [Some cool hacks we've seen from hackathons](README.md#some-cool-hacks-weve-seen-from-hackathons)
* [Tips](README.md#tips)

## Why does Twilio sponsor hackathons?
- To inspire and equip developers, mentoring and teaching you about Twilio as well as general programming topics unrelated to Twilio products!
- To create evangelists, champions out of developers by getting you excited to use Twilio!
- Receive product feedback and see different use cases. Be creative! :D 
- Yes, to generate more sign-ups. We are a public company after all!
- Yes, it does look good in a Twilio interview to "eat the API dog food" and have experience using Twilio products--so use Twilio in your hacks and you can talk about it in interviews. Some former "Best use of Twilio" hackathon winners went on to intern here! Check out our [job listings](https://twilio.com/jobs)

## TODO before the hackathon
We recommend playing through [TwilioQuest](https://twilio.com/quest), a video game that makes it fun to learn how to use different Twilio products. There's also lots of tutorials and documentation you can read through (see below.)

## TODO after the hackathon
Make sure to put your hack on GitHub (public) for the world to see and submit to DevPost! This will come in handy for interviews and more. 
Go back and clean up the code, make a good README, and continue iterating over your hack if you are passionate about it and want to add on different features. The sky is the limit! 

## Get started
1. [Make a Twilio account (it's free!)](https://www.twilio.com/try-twilio)
2. [Apply promo code](https://twil.io/apply-promo)
3. [Buy a Twilio phone number](https://www.twilio.com/console/phone-numbers/incoming)
4. Configure your Twilio phone number for when a SMS or phone call comes in with a [TwiML Bin](https://www.twilio.com/console/twiml-bins), [Twilio Function](https://www.twilio.com/console/functions), or [ngrok](https://ngrok.io) URL. 

## Quick and easy code snippets
Did you miss the Twilio demo during the hackathon Opening Ceremony? It probably contained code like this:

### Node.js code to respond to texts 
```js
var express = require('express');
var bodyParser = require('body-parser');
var dotenv = require('dotenv');
dotenv.load();

var app = express();
app.use(bodyParser.urlencoded({extended: false}));
app.post('/hack', (req, res) => {
    var inbMsg = req.body.Body.toLowerCase().trim();
    if(inbMsg == "matcha") {
        res.send("<Response><Message>Responding to matcha</Message></Response>");
    }
    res.send("<Response><Message>Else respond with this</Message></Response>");
});

app.listen(1337, () => {
    console.log("Express server listening on port 1337");
});
```

### Node.js code to make a phone call to every number that texted your Twilio number
```js
var express = require('express');
var bodyParser = require('body-parser');
var dotenv = require('dotenv');
dotenv.load();
var fromNum = "your-twilio-number";

var app = express();
app.use(bodyParser.urlencoded({extended: false}));
const client = require('twilio')('YOUR-ACCOUNT-SID', 'YOUR-AUTH-TOKEN');
const filter = {
    to: fromNum // switch this out with your "from" number
}
client.messages.each(filter, (message) => client.calls.create({
    url: 'https://desolate-shelf-95000.herokuapp.com/redirect', // switch this for the mp3 of your choice
    to: message.from,
    from: fromNum // again, switch out for your "from" number
}).then(call => console.log(call.sid)));
```

### Node.js code in a [Twilio Function](https://twilio.com/console/functions)
```js
exports.handler = function(context, event, callback) {
	let twiml = new Twilio.twiml.MessagingResponse();
	if(event.Body.toLowerCase().trim() == "matcha") {
        twiml.message("You right. @lizziepika, lsiegle@twilio.com, promo: HACKUCI2020, https://twil.io/hackathons");
    }
    else {
        twiml.message("No. @lizziepika, lsiegle@twilio.com, promo: HACKUCI2020, https://twil.io/hackathons");
    }
	callback(null, twiml);
};
```

### Python code to respond to texts 
```python
from twilio.twiml.messaging_response import MessagingResponse
from flask import Flask, request

app = Flask(__name__)
@app.route('/sms', methods=['GET', 'POST'])
def sms():
    msg = request.values.get('Body').lower().strip()
    res = MessagingResponse()
    if msg == "matcha":
        res.message("noice")
    else:
        res.message("meh")
    return str(res)

if __name__ == "__main__":
    app.run(debug=True)
```
### Python code to make a phone call to every number that texted your Twilio number
```python
from twilio.rest import Client

client = Client('YOUR-TWILIO-ACCOUNT-SID', 'YOUR-TWILIO-AUTH-TOKEN')
for num in client.messages.list(to='YOUR-TWILIO-NUMBER'):
    call = client.calls.create(
        url = 'http://demo.twilio.com/docs/classic.mp3',
        to = num.from_,
        from_ = 'YOUR-TWILIO-NUMBER'
        )
    print(call.sid)
```
## Tutorials
### by product
- [SMS docs](https://www.twilio.com/docs/sms)
- [Voice docs](https://www.twilio.com/docs/voice)
- [Video tutorials](https://www.twilio.com/docs/video/tutorials)
- [Autopilot blog posts](https://www.twilio.com/docs/autopilot/blog-posts)

### by language
#### Node.js
- [send sms and mms in Node.js](https://www.twilio.com/docs/sms/tutorials/how-to-send-sms-messages-node-js)
- [SMS Node.js quickstart](https://www.twilio.com/docs/sms/quickstart/node)
- [Voice Node.js quickstart](https://www.twilio.com/docs/voice/quickstart/node)
- [Video quickstart for JS](https://github.com/twilio/video-quickstart-js)

#### React.js
- [Send an SMS from React with Twilio](https://www.twilio.com/blog/send-an-sms-react-twilio)

#### Python
- [send SMS and MMS in Python](https://www.twilio.com/docs/sms/tutorials/how-to-send-sms-messages-python)
- [SMS Python quickstart](https://www.twilio.com/docs/sms/quickstart/python)
- [Voice Python quickstart](https://www.twilio.com/docs/voice/quickstart/node)

#### Swift
- [chat in Swift](https://www.twilio.com/docs/chat/tutorials/chat-application-ios-swift)
- [SMS in Swift](https://www.twilio.com/blog/2018/03/sending-text-messages-in-swift-with-twilio.html)
- [iOS quickstart](https://www.twilio.com/docs/chat/ios/quickstart)

#### Java
- [Android quickstart](https://www.twilio.com/docs/voice/client/android/quickstart/php) 
- [Twilio Java library](https://github.com/twilio/twilio-java)
- [Java SMS quickstart](https://www.twilio.com/docs/sms/quickstart/java)
- [send SMS, MMS in Java](https://www.twilio.com/docs/sms/tutorials/how-to-send-sms-messages-java)
- [receive, reply to SMS, MMS in Java](https://www.twilio.com/docs/sms/tutorials/how-to-receive-and-reply-java)
- [voice quickstart in Java](https://www.twilio.com/docs/voice/quickstart/java)
- [respond to incoming phone calls in Java](https://www.twilio.com/docs/voice/tutorials/how-to-respond-to-incoming-phone-calls-java)
- [modify in-progress calls in Java](https://www.twilio.com/docs/voice/tutorials/how-to-modify-calls-in-progress-java)
- [make outbound calls in Java](https://www.twilio.com/docs/voice/tutorials/how-to-make-outbound-phone-calls-java)
- [Chat tutorial for Android and Java](https://www.twilio.com/docs/chat/tutorials/chat-application-android-java)
- [Twilio Video quickstart for Android](https://github.com/twilio/video-quickstart-android)

#### YouTube videos
- [Build an IVR with Twilio Studio](https://www.youtube.com/watch?v=GifYSpB-EU4)
- [Make + receive phone calls in Node.js](https://www.youtube.com/watch?v=CgNd6VgNzDk)
- [Send + receive SMS in Node.js](https://www.youtube.com/watch?v=f9jE5ywz8cs)
- [Send + receive SMS in Python](https://www.youtube.com/watch?v=knxlmCVFAZI)
- [Make + receive phone calls in Python](https://www.youtube.com/watch?v=-AChTCBoTUM)
- [Send + reply to SMS in Java 8 and Spark](https://www.youtube.com/watch?v=jdlWQtgsNSU)
- [Send email with Java and SendGrid](https://www.youtube.com/watch?v=06M3lZzZEMY&list=PLqrz4nXepkz5IpQFH81FcvknWgnKf50DH&index=30)
- [Send email with Python and SendGrid](https://www.youtube.com/watch?v=xCCYmOeubRE&list=PLqrz4nXepkz5IpQFH81FcvknWgnKf50DH&index=29)
- [Send a WhatsApp Message in Python](https://www.youtube.com/watch?v=98OewpG8-yw&list=PLqrz4nXepkz5IpQFH81FcvknWgnKf50DH&index=27)
- [Send a WhatsApp message in Node.js](https://www.youtube.com/watch?v=PxphXQmtHLo&list=PLqrz4nXepkz5IpQFH81FcvknWgnKf50DH&index=25)
- [Send an SMS in Kotlin](https://www.youtube.com/watch?v=uThgVuAEKgU&list=PLqrz4nXepkz5IpQFH81FcvknWgnKf50DH&index=18)
- [Image recognition in Python with Clarifai and Twilio MMS](https://www.youtube.com/watch?v=18KQIPhiVdc)
- [Basics of making + receiving phone calls](https://www.youtube.com/watch?v=Yf9JkKmeO8U)
- [Basics of sending + receiving text messages](https://www.youtube.com/watch?v=344S512CoP0)
- [Send and reply to text messages in Java](https://www.youtube.com/watch?v=jdlWQtgsNSU)
- [Build SMS surveys in Twilio Studio](https://www.youtube.com/watch?v=iTZRooIdy6U)
- [Build call forwarding apps with Twilio Studio](https://www.youtube.com/watch?v=atshc8I-AjA)
- [How to post messages to Slack with Twilio Studio](https://www.youtube.com/watch?v=wMExZ3yq3Vk)

#### Docs

- [Send SMS with Twilio Programmable Messaging](- [How to post messages to Slack with Twilio Studio](https://www.youtube.com/watch?v=wMExZ3yq3Vk)

## Some cool hacks we've seen from hackathons
- [smtex from MHacks 11](https://devpost.com/software/smtex)
- [Moist Meter from MHacks 11](https://devpost.com/software/moist-meter)

<img src="https://lh4.googleusercontent.com/Y6SBPai2KslqW5Pwzv0B6teL16vwiiItKTbS5gPsDG2FxPN0iC9aklIbXM6aLq28RKHipc6Kd46VGanaidDAptHhvy2ouDFmVpezp8oYvf2FQrJgmD9ANQDtnucb2n4XKDwuhzKf" alt="moist meter pic" width="300" height="450"/>

- [Health Hunt AR from TreeHacks 2019](https://devpost.com/software/healthhunt-ar)

<img src="https://challengepost-s3-challengepost.netdna-ssl.com/photos/production/software_photos/000/766/426/datas/gallery.jpg" alt="health hunt ar pic" height="450"/>

## Tips 
We've been to a lot of hackathons, both as hackers and sponsors. What advice do we have for you as hackers?
- **Have fun!** Hackathons can be intense and a lot to handle. Don't forget to build something you want to build.
- **Take risks!** Learn something new. Try building something in a new language. You're surrounded by passionate people who are giving up their weekends to build something or help you. Take advantage of them! Ask questions about what classes they're taking if they're a fellow hacker, or talk to a mentor/sponsor about their jobs and their backgrounds.
- **Go to workshops and activities.** Yes, you're probably here to hack, but you can't be productive for the whole time. Don't forget to take breaks, talk to people, and take advantage of what the organizers have put together for you.
- **Demo.** Even if your hack isn't perfect, it's a hack. You had a weekend to build something and hopefully you did other things, too (maybe cup-stacking?) Prepare a demo and give it! It's fun and important to be able to explain what you did and to show others.
    - On the topic of demos, keep it short and simple. Yes, it's nice to have a lead-in showing you did background research, but the focus should be on showing what you built. That is the primary focus of judges: most everything else is probably secondary.

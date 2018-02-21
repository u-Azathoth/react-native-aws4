AWS4 React Native
-----------------
![GitHub Logo](http://image.ibb.co/hs8Pnc/logo.jpg)

**NOTE**: This package is a stabe fork of aws4 and aws4-react-native modified to work with React Native apps. With the most important change - fix Buffer dependencies. The core Node JS module `querystring` has been replaced by [`querystring-browser`](https://www.npmjs.com/package/querystring-browser), and `crypto` has been replaced by a standalone javascript file [`crypto.js`](./crypto.js) generated using [browserify](http://browserify.org/).

What follows is the a slighly modified README from [`aws4`](https://www.npmjs.com/package/aws4).

<hr/>

Example
-------

```javascript
import aws4 from 'react-native-aws4';

// given an options object you could pass to http.request
const opts = {
  host: 'sqs.us-east-1.amazonaws.com',
  path: '/?Action=ListQueues'
};

// alternatively (as aws4 can infer the host):
opts = {
  service: 'sqs', 
  region: 'us-east-1', 
  path: '/?Action=ListQueues'
}

// alternatively (as us-east-1 is default):
opts = {
  service: 'sqs', 
  path: '/?Action=ListQueues'
}

aws4.sign(opts) // assumes AWS credentials are available in process.env

console.log(opts)
/*
{
  host: 'sqs.us-east-1.amazonaws.com',
  path: '/?Action=ListQueues',
  headers: {
    Host: 'sqs.us-east-1.amazonaws.com',
    'X-Amz-Date': '20121226T061030Z',
    Authorization: 'AWS4-HMAC-SHA256 Credential=ABCDEF/20121226/us-east-1/sqs/aws4_request, ...'
  }
}
*/

// we can now use this to query AWS using the standard React Native API
const url = "https://" + signedOptions.host + signedOptions.path;
fetch(url, signedOptions)
  .then(body => body.json())
  .then(json => console.log(json));
// The above code is equivalent to the following Node JS request:
// http.request(opts, function(res) { res.pipe(process.stdout) }).end()
/*
*/
```

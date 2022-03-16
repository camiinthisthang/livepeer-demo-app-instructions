# Getting Started with the Livepeer Demo App
Prerequisites:
- Have an account with Livepeer and create an API key. You can do that [here.](https://livepeer.com/dashboard/developers/api-keys)
- Understand how HTTP requests work. For a beginner-friendly lesson, [check on this article I wrote for Free Code Camp.](https://www.freecodecamp.org/news/ghost/#/site)

## Running The App Locally 

1. Head to the [Github repo for this project.](https://github.com/livepeer/livepeer-demo-app)

2. Hit the "Code" button at the top left, opening up a drop down menu.
<img width="379" alt="Screen Shot 2022-03-13 at 7 28 57 PM" src="https://user-images.githubusercontent.com/15346823/158081890-b712276f-5b69-488c-be85-270530b667c9.png">

3. Copy the link provided.

4. In your terminal, navigate to the folder where you wan to save this repo. I'll be in Desktop. Once there run the following command to clone the codebase to your local machine: ```https://github.com/livepeer/livepeer-demo-app```

5. Change directories into the new project by using this command in the terminal: ```git clone https://github.com/livepeer/livepeer-demo-app.git``` That link is copied from step 3.

6.  Run the following command in your terminal to install the dependecies needed for this project: ```yarn```

7. Run the following command in the terminal to install all dependencies: ```yarn build``` & then do ```yarn start```.

8. Navigate to the URL where your project is running. Here you will paste in your API key that you created>
<img width="745" alt="Screen Shot 2022-03-13 at 7 41 01 PM" src="https://user-images.githubusercontent.com/15346823/158082259-373c5114-a1c5-44da-a79d-5f6aed0ea78d.png">

9. Hit "Create Stream" 
<img width="172" alt="Screen Shot 2022-03-13 at 7 41 31 PM" src="https://user-images.githubusercontent.com/15346823/158082273-d2d59431-df77-4d8e-9030-8d61d4e467d5.png">

10. You'll be given a stream key which you can use to stream from OBS. There is also experimental support for broswer streaming with JustCastIt. You can use the browser streaming client on a chrome browser by navigating to: justcastit.io/to/{your-stream-key-here}.

<img width="964" alt="Screen Shot 2022-03-13 at 7 44 20 PM" src="https://user-images.githubusercontent.com/15346823/158082375-37fee140-473c-4ecc-87f4-77eb56513ede.png">


## How The App Works 

From the [Livepeer API Docs:](https://livepeer.com/docs/api-reference/stream/post-stream)
The stream object is the core building block of the Livepeer.com API.

A Livepeer.com stream is a unique object with configuration data and metadata about all live stream sessions associated with it.

The stream object parameters associated with configuration settings are read-write, for example changing the record value to turn recording on or off for future sessions.

Other stream object parameters are read only. These include the unique id, ingested sourceSegments and duration data, among others.

### The backend

In [Next.js](https://nextjs.org/), the React framework we're using for this demo applications, you can create API routes directly in your app inside the ```pages``` folder. To create a stream, we define an API route called ```stream``` where we create an asynchronous handler function that takes in a request to this API route:
```js
export default async (req, res) => {
  if (req.method === "POST") {
    const authorizationHeader = req.headers && req.headers["authorization"];
    const streamName = req.body && req.body.name;
    const streamProfiles = req.body && req.body.profiles;
```
If the request method is POST, it sets the headers and other fields to create a stream. 

```js
try {
      const createStreamResponse = await axios.post(
        "https://livepeer.com/api/stream",
        {
          name: streamName,
          profiles: streamProfiles,
        },
        {
          headers: {
            "content-type": "application/json",
            authorization: authorizationHeader, // API Key needs to be passed as a header
          },
        }
      );
```

### The Frontend
In order to create a stream, the creator needs to enter their API key. This app should be usable for any creator to use, therefore we dont hardcode an API key. Aside from making the app flexible, you should never store your API key in your app because it could be exposed to malicious users who could access your streams with this key. In the front end, we have a textbox where we ask the user to enter their API key, and then we make the request to the API using their information.

```js
import axios from "axios";

const apiInstance = axios.create({
  baseURL: "/api/",
  timeout: 10000,
});

export const createStream = (apiKey: string): Promise<any> => {
  return apiInstance.post(
    "/stream",
    {
      name: "test_stream",
      profiles: [
        {
          name: "720p",
          bitrate: 2000000,
          fps: 30,
          width: 1280,
          height: 720,
        },
        {
          name: "480p",
          bitrate: 1000000,
          fps: 30,
          width: 854,
          height: 480,
        },
        {
          name: "360p",
          bitrate: 500000,
          fps: 30,
          width: 640,
          height: 360,
        },
      ],
    },
    {
      headers: {
        "content-type": "application/json",
        authorization: `Bearer ${apiKey}`,
      },
    }
  );
};

export const getStreamStatus = (
  apiKey: string,
  streamId: string
): Promise<any> => {
  return apiInstance.get(`/stream/${streamId}`, {
    headers: {
      "content-type": "application/json",
      authorization: `Bearer ${apiKey}`,
    },
  });
};
```

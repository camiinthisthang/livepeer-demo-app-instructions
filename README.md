# Getting Started with the Livepeer Demo App
Prerequisites:
- Have an account with Livepeer and create an API key. You can do that [here.](https://livepeer.com/dashboard/developers/api-keys)


1. Head to the [Github repo for this project.](https://github.com/livepeer/livepeer-demo-app)
2. Hit the "Code" button at the top left, opening up a drop down menu.
<img width="379" alt="Screen Shot 2022-03-13 at 7 28 57 PM" src="https://user-images.githubusercontent.com/15346823/158081890-b712276f-5b69-488c-be85-270530b667c9.png">
3. Copy the link provided.
4. In your terminal, navigate to the folder where you wan to save this repo. I'll be in Desktop. Once there run the following command to clone the codebase to your local machine: ```https://github.com/livepeer/livepeer-demo-app```
5. Change directories into the new project by using this command in the terminal: ```git clone https://github.com/livepeer/livepeer-demo-app.git``` That link is copied from step 3.
6.  Run the following command in your terminal to install the dependecies needed for this project: ```yarn```
7. Run the following command in the terminal to install all dependencies: ```yarn build```
8. Navigate to the URL where your project is running. Here you will paste in your API key that you created>
<img width="745" alt="Screen Shot 2022-03-13 at 7 41 01 PM" src="https://user-images.githubusercontent.com/15346823/158082259-373c5114-a1c5-44da-a79d-5f6aed0ea78d.png">
9. Hit "Create Stream" 
<img width="172" alt="Screen Shot 2022-03-13 at 7 41 31 PM" src="https://user-images.githubusercontent.com/15346823/158082273-d2d59431-df77-4d8e-9030-8d61d4e467d5.png">
10. You'll be given a stream key which you can use to stream from OBS. There is also experimental support for broswer streaming with JustCastIt. You can use the browser streaming client on a chrome browser by navigating to: justcastit.io/to/{your-stream-key-here}.

<img width="964" alt="Screen Shot 2022-03-13 at 7 44 20 PM" src="https://user-images.githubusercontent.com/15346823/158082375-37fee140-473c-4ecc-87f4-77eb56513ede.png">

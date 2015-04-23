# Social Authentication

- [Quickstart](#quickstart)
- [Facebook](#facebook)
- [Google](#google)
- [Twitter](#twitter)
- [LinkedIn](#linkedin)
- [Microsoft](#microsoft)
- [Instagram](#instagram)
- [GitHub](#github)
- [Yammer](#yammer)
- [Foursquare](#foursquare)
- [SoundCloud](#soundcloud)
- [VK](#vk)

## Quickstart

Social Authentication allows the users of your website to log in with their 
[Facebook](https://www.facebook.com)
[Google+](https://plus.google.com)
[Twitter](https://twitter.com)
[LinkedIn](https://www.linkedin.com)
[Microsoft](https://login.live.com)
[Instagram](http://instagram.com)
[GitHub](https://github.com)
[Yammer](http://yammer.com)
[Foursquare](https://foursquare.com)
[SoundCloud](https://soundcloud.com) and
[VK](https://vk.com)  accounts.

To enable them first open `app/config/auth.php` and add them to the `providers` array like this:

    'providers' => array(
        'facebook' => 'Facebook', 
        'google'   => 'Google', 
        'twitter'  => 'Twitter', 
        'linkedin' => 'LinkedIn',
        // 'microsoft' => 'Microsoft',
        // 'instagram' => 'Instagram',
        // 'github' => 'GitHub',
        // 'yammer' => 'Yammer',
        // 'foursquare' => 'Foursquare',
        // 'soundcloud' => 'SoundCloud',
        // 'vkontakte' => 'VK'
    ),

Next, you'll have to set the API keys. Open `app/config/services.php` and set the `id` and `secret` for each one. Follow the instructions below for each of the services.

## Facebook

<p class="video-wrapper"><iframe allowfullscreen="1" frameborder="0" src="http://www.youtube.com/embed/10afuqFenVY?rel=0&showinfo=0&vq=hd720"></iframe></p>

Go to <a href="https://developers.facebook.com" target="_blank">Facebook Developers</a>, click on __Apps__ > __Create a New App__ (if you are not a developer you'll have to click on the __Register as a Developer__ to register your developer account), pick a Name and Category and click __Create App__. 

Once the app is created click on the __Settings__ tab and set the __App Domains__ to your website domain (leave it empty if you are working on your localhost server) and __Contact Email__ to your email address. 

Then click on the __+ Add Platform__ button, select __Website__ and new section will apear. Set the __Site URL__ to the url that points to the `oauth.php` file, like this: `http://yourwebsite.com/oauth.php?provider=facebook`. Click __Save Changes__ to save your app settings.

Move to the __Status & Review__ tab and make the app public (or leave it like that if you are just testing).

Finaly go back to the __Settings__ tab and copy the __App ID__ and __App Secret__ to `app/config/services.php` under the `facebook` section like this:

    'facebook' => array(
        'id' => 'your-app-id',
        'secret' => 'your-app-secret'
    ),

## Google

<p class="video-wrapper"><iframe allowfullscreen="1" frameborder="0" src="http://www.youtube.com/embed/tnbvTEsuTaw?rel=0&showinfo=0&vq=hd720"></iframe></p>

Go to <a href="https://console.developers.google.com/project" target="_blank">Google Developers Console</a>, click on __Create Project__, pick a Name and click __Create__.

Once the project is created click on the __Enable an API__ button and a list will show. Look for __Google+ API__ and enable it. Next go to the __Credentials__ tab (under __APIs & auth__) and click on the __Create new Client ID__ button. 

Select __Web application__, set the __Authorized JavaScript origins__ to your website url and __Authorized redirect URI__ to the url that points to the `oauth.php` file, like this: `http://yourwebsite.com/oauth.php?provider=google`. Click __Create Client ID__ and a new __Client ID for web application__ will be created.

Finaly copy the __CLIENT ID__ and __CLIENT SECRET__ to `app/config/services.php` under the `google` section like:

    'google' => array(
        'id' => 'your-client-id',
        'secret' => 'your-client-secret'
    ),

## Twitter

<p class="video-wrapper"><iframe allowfullscreen="1" frameborder="0" src="http://www.youtube.com/embed/to1AXq4MCKk?rel=0&showinfo=0&vq=hd720"></iframe></p>

Go to <a href="https://dev.twitter.com" target="_blank">Twitter Developers</a>, click on __My applications__ under your profile picture and then click on the __Create New App__ button. Pick a Name, Description, set the __Website__ to your website url and the __Callback URL__ to the url that points to the `oauth.php` file, like this: `http://yourwebsite.com/oauth.php?provider=twitter` and click on the __Create your Twitter application__ button.

Once the app is created go to the __API Keys__ tab and copy __API key__ and __API secret__ to `app/config/services.php` under the `twitter` section like this:

    'twitter' => array(
        'id' => 'your-api-key',
        'secret' => 'your-api-secret'
    ),

## LinkedIn

<p class="video-wrapper"><iframe allowfullscreen="1" frameborder="0" src="http://www.youtube.com/embed/NoRSfagg3RU?rel=0&showinfo=0&vq=hd720"></iframe></p>

Go to <a href="https://developer.linkedin.com" target="_blank">LinkedIn Developers</a>, click on __API Keys__ under your profile name and then click on the __Add New Application__ button. 

Complete the required fields with information about the app, then for __Default Scope__ check __r_fullprofile__, __r_emailaddress__, __r_contactinfo__ and  set the __OAuth 2.0 Redirect URLs__ and __OAuth 1.0 Accept Redirect URL__ to the url that points to the `oauth.php` file, like this: `http://yourwebsite.com/oauth.php?provider=linkedin` and click on the __Add Application__ button.

Once the app is created copy __API Key__ and __Secret Key__ to `app/config/services.php` under the `linkedin` section like this:

    'linkedin' => array(
        'id' => 'your-api-key',
        'secret' => 'your-secret-key'
    ),

## Microsoft

<p class="video-wrapper"><iframe allowfullscreen="1" frameborder="0" src="http://www.youtube.com/embed/HAoPHQS7DJA?rel=0&showinfo=0&vq=hd720"></iframe></p>

Go to <a href="https://account.live.com/developers/applications/index" target="_blank">Microsoft Developers</a>, click on __Create application__, pick a Name for the app and click on the __I accept__ button.

Once the app is created go to the __API Settings__ tab and set __Redirect URLs__ to to the url that points to the `oauth.php` file, like this: `http://yourwebsite.com/oauth.php?provider=microsoft` and click on the __Save__ button. 

Finaly go to the __App Settings__ tab and copy __Client ID__ and __Client secret__ to `app/config/services.php` under the `microsoft` section like this:

    'microsoft' => array(
        'id' => 'your-client-id',
        'secret' => 'your-client-secret'
    ),

## Instagram

Go to <a href="http://instagram.com/developer/clients/manage/" target="_blank">Instagram Developers</a> and click on the __Register a New Client__ button. Pick a Name, Description and enter your Website url, then set __OAuth redirect_uri__ to to the url that points to the `oauth.php` file, like this: `http://yourwebsite.com/oauth.php?provider=instagram` and click on the __Register__ button. 

Once the client is created copy __CLIENT ID__ and __CLIENT SECRET__ to `app/config/services.php` under the `instagram` section like this:

    'instagram' => array(
        'id' => 'your-client-id',
        'secret' => 'your-client-secret'
    ),

## GitHub

Go to <a href="https://github.com/settings/applications" target="_blank">GitHub Developers</a> and click on the __Register new application__ button. Pick a Name, Descroption and enter your Homepage url, then set __Authorization callback URL__ to the url that points to the `oauth.php` file, like this: `http://yourwebsite.com/oauth.php?provider=github` and click on the __Register application__ button.

Once the app is created copy __Client ID__ and __Client Secret__ to `app/config/services.php` under the `github` section like this:

    'github' => array(
        'id' => 'your-client-id',
        'secret' => 'your-client-secret'
    ),

## Yammer

Go to <a href="https://www.yammer.com/client_applications" target="_blank">Yammer Developers</a>, click on the __Register New App__ button, pick a Name, Email, enter your Website url and click __Continue__.

Next, click on the __Basic Info__ tab and set __Redirect URI__ to the url that points to the `oauth.php` file, like this: `http://yourwebsite.com/oauth.php?provider=yammer` and click on the __Save__ button.

Finaly click on the app name and copy __Client ID__ and __Client secret__ to `app/config/services.php` under the `yammer` section like this:

    'yammer' => array(
        'id' => 'your-client-id',
        'secret' => 'your-client-secret'
    ),

## Foursquare

Go to <a href="https://foursquare.com/developers/apps" target="_blank">Foursquare Developers</a> and click on the __Create a new app__ button. 

Pick a Name, enter your Website url, and set __Redirect URI__ to the url that points to the `oauth.php` file, like this: `http://yourwebsite.com/oauth.php?provider=foursquare` and click on the __Save changes__ button.

Once the app is created copy __Client id__ and __Client secret__ to `app/config/services.php` under the `foursquare` section like this:

    'foursquare' => array(
        'id' => 'your-client-id',
        'secret' => 'your-client-secret'
    ),

## SoundCloud

Go to <a href="http://soundcloud.com/you/apps" target="_blank">SoundCloud Apps</a>, click on the __Register a new application__ button, pick a Name and click __Register__

Once the app is created enter your Website url, then set __Redirect URI__ to the url that points to the `oauth.php` file, like this: `http://yourwebsite.com/oauth.php?provider=soundcloud` and click on the __Save app__ button.

Finaly copy __Client ID__ and __Client Secret__ to `app/config/services.php` under the `soundcloud` section like this:

    'soundcloud' => array(
        'id' => 'your-client-id',
        'secret' => 'your-client-secret'
    ),

## VK

Go to <a href="https://vk.com/apps?act=manage" target="_blank">VK Apps</a>, click on the __Create an Application__ button, pick a Title, set the __Category__ to Website, enter your Website url and lick __Connect Site__. You'll be asked to enter you phone number so they can send you a confirmation code.

Once the app is created go to the __Settings__ tab and set __First API request__ to to the url that points to the `oauth.php` file, like this: `http://yourwebsite.com/oauth.php?provider=vkontakte` and click on the __Save__ button.

Finaly copy __Application ID__ and __Secure key__ to `app/config/services.php` under the `vkontakte` section like this:

    'vkontakte' => array(
        'id' => 'your-application-id',
        'secret' => 'your-secure-key'
    ),

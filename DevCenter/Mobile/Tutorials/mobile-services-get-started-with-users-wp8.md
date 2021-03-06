<properties linkid="mobile-get-started-with-users-dotnet" urldisplayname="Mobile Services" headerexpose="" pagetitle="Get started with authentication in Mobile Services" metakeywords="Get started Windows Azure Mobile Services, mobile devices, Windows Azure, mobile, Windows 8, WinRT app" footerexpose="" metadescription="Get started using Windows Azure Mobile Services in your Windows Phone apps." umbraconavihide="0" disquscomments="1"></properties>




# Get started with authentication in Mobile Services
<div class="dev-center-tutorial-selector sublanding"> 
	<a href="/en-us/develop/mobile/tutorials/get-started-with-users-dotnet" title="Windows Store C#">Windows Store C#</a><a href="/en-us/develop/mobile/tutorials/get-started-with-users-js" title="Windows Store JavaScript">Windows Store JavaScript</a><a href="/en-us/develop/mobile/tutorials/get-started-with-users-wp8" title="Windows Phone" class="current">Windows Phone</a><a href="/en-us/develop/mobile/tutorials/get-started-with-users-ios" title="iOS">iOS</a><a href="/en-us/develop/mobile/tutorials/get-started-with-users-android" title="Android">Android</a><a href="/en-us/develop/mobile/tutorials/get-started-with-users-html" title="HTML">HTML</a><a href="/en-us/develop/mobile/tutorials/get-started-with-users-xamarin-ios" title="Xamarin.iOS">Xamarin.iOS</a><a href="/en-us/develop/mobile/tutorials/get-started-with-users-xamarin-android" title="Xamarin.Android">Xamarin.Android</a>
</div>


<div class="dev-onpage-video-clear clearfix">
<div class="dev-onpage-left-content">

<p>This topic shows you how to authenticate users in Windows Azure Mobile Services from your app. In this tutorial, you add authentication to the quickstart project using an identity provider that is supported by Mobile Services. After being successfully authenticated and authorized by Mobile Services, the user ID value is displayed.</p>
</div>
<div class="dev-onpage-video-wrapper"><a href="http://go.microsoft.com/fwlink/?LinkId=298631" target="_blank" class="label">watch the tutorial</a> <a style="background-image: url('/media/devcenter/mobile/videos/mobile-wp8-get-started-authentication-180x120.png') !important;" href="http://go.microsoft.com/fwlink/?LinkId=298631" target="_blank" class="dev-onpage-video"><span class="icon">Play Video</span></a> <span class="time">10:50</span></div>
</div>  

This tutorial walks you through these basic steps to enable authentication in your app:

1. [Register your app for authentication and configure Mobile Services]
2. [Restrict table permissions to authenticated users]
3. [Add authentication to the app]

This tutorial is based on the Mobile Services quickstart. You must also first complete the tutorial [Get started with Mobile Services]. 

<h2><a name="register"></a><span class="short-header">Register your app</span>Register your app for authentication and configure Mobile Services</h2>

To be able to authenticate users, you must register your app with an identity provider. You must then register the provider-generated client secret with Mobile Services.

1. Log on to the [Windows Azure Management Portal], click **Mobile Services**, and then click your mobile service.

   ![][1]

2. Click the **Dashboard** tab and make a note of the **Mobile Service URL** value.

   ![][2]

    You may need to provide this value to the identity provider when you register your app.

3. Choose a supported identity provider from the list below and follow the steps to register your app with that provider:

 - <a href="/en-us/develop/mobile/how-to-guides/register-for-microsoft-authentication/" target="_blank">Microsoft Account</a>
 - <a href="/en-us/develop/mobile/how-to-guides/register-for-facebook-authentication/" target="_blank">Facebook login</a>
 - <a href="/en-us/develop/mobile/how-to-guides/register-for-twitter-authentication/" target="_blank">Twitter login</a>
 - <a href="/en-us/develop/mobile/how-to-guides/register-for-google-authentication/" target="_blank">Google login</a>

    Remember to make a note of the client identity and secret values generated by the provider.

    <div class="dev-callout"><b>Security Note</b>
	<p>The provider-generated secret is an important security credential. Do not share this secret with anyone or distribute it with your app.</p>
    </div>

4. Back in the Management Portal, click the **Identity** tab, enter the app identifier and shared secret values obtained from your identity provider, and click **Save**.

   ![][3]

Both your mobile service and your app are now configured to work with your chosen authentication provider.

<h2><a name="permissions"></a><span class="short-header">Restrict permissions</span>Restrict permissions to authenticated users</h2>

1. In the Management Portal, click the **Data** tab, and then click the **TodoItem** table. 

   ![][4]

2. Click the **Permissions** tab, set all permissions to **Only authenticated users**, and then click **Save**. This will ensure that all operations against the **TodoItem** table require an authenticated user. This also simplifies the scripts in the next tutorial because they will not have to allow for the possibility of anonymous users.

   ![][5]

3. In Visual Studio 2012 Express for Windows Phone, open the project that you created when you completed the tutorial [Get started with Mobile Services]. 

4. Press the F5 key to run this quickstart-based app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts. 
   
   This happens because the app attempts to access Mobile Services as an unauthenticated user, but the _TodoItem_ table now requires authentication.

Next, you will update the app to authenticate users before requesting resources from the mobile service.

<h2><a name="add-authentication"></a><span class="short-header">Add authentication</span>Add authentication to the app</h2>

5. Open the project file mainpage.xaml.cs and add the following code snippet to the MainPage class:
	
        private MobileServiceUser user;
        private async System.Threading.Tasks.Task Authenticate()
        {
            while (user == null)
            {
                string message;
                try
                {
                    user = await App.MobileService
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
                    message =
                        string.Format("You are now logged in - {0}", user.UserId);
                }
                catch (InvalidOperationException)
                {
                    message = "You must log in. Login Required";
                }

                MessageBox.Show(message);
            }
        }

    This creates a member variable for storing the current user and a method to handle the authentication process. The user is authenticated by using a Facebook login.

    <div class="dev-callout"><b>Note</b>
	<p>If you are using an identity provider other than Facebook, change the value of <strong>MobileServiceAuthenticationProvider</strong> above to the value for your provider.</p>
    </div>

8. Delete or comment-out the existing **OnNavigatedTo** method override and replace it with the following method that handles the **Loaded** event for the page. 

        async void MainPage_Loaded(object sender, RoutedEventArgs e)
        {
            await Authenticate();
            RefreshTodoItems();
        }

   This method calls the new **Authenticate** method. 

9. Replace the MainPage constructor with the following code:

        // Constructor
        public MainPage()
        {
            InitializeComponent();
            this.Loaded += MainPage_Loaded;
        }

   This constructor also registers the handler for the Loaded event.
		
10. Press the F5 key to run the app and sign into the app with your chosen identity provider. 

   When you are successfully logged-in, the app should run without errors, and you should be able to query Mobile Services and make updates to data.

## <a name="next-steps"> </a>Next steps

In the next tutorial, [Authorize users with scripts], you will take the user ID value provided by Mobile Services based on an authenticated user and use it to filter the data returned by Mobile Services. 

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions to authenticated users]: #permissions
[Add authentication to the app]: #add-authentication
[Next Steps]:#next-steps

<!-- Images. -->
[1]: ../Media/mobile-services-selection.png
[2]: ../Media/mobile-service-uri.png
[3]: ../Media/mobile-identity-tab.png
[4]: ../Media/mobile-portal-data-tables.png
[5]: ../Media/mobile-portal-change-table-perms.png

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[Get started with Mobile Services]: ./mobile-services-get-started-wp8.md
[Get started with data]: ./mobile-services-get-started-with-data-wp8.md
[Get started with authentication]: ./mobile-services-get-started-with-users-wp8.md
[Get started with push notifications]: ./mobile-services-get-started-with-push-wp8.md
[Authorize users with scripts]: ./mobile-services-authorize-users-wp8.md
[WindowsAzure.com]: http://www.windowsazure.com/
[Windows Azure Management Portal]: https://manage.windowsazure.com/
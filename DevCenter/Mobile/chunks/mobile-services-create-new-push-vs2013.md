First, you use the Add Push Notification wizard in Visual Studio 2013 to register your app with the Windows Store, configure your mobile service to enable push notifications, and add code to your app to register a device channel.

1. In Visual Studio 2013, open Solution Explorer, right-click the project, click **Add** then **Push Notification...**. 

	<img src="../Media/mobile-add-push-notifications-vs2013.png" />

	This starts the Add Push Notification Wizard.

2. Click **Next**, sign in to your Windows Store account, then supply a name in **Reserve a new name** and click **Reserve**.

	<img src="../Media/mobile-add-push-notifications-vs2013-2.png" /> 

	This create a new app registration.

3. Click the new registration in the **App Name** list, then click **Next**.

	<img src="../Media/mobile-add-push-notifications-vs2013-3.png" />

4. Click the name of the mobile service that you created when you completed either [Get started with Mobile Services] or [Get started with data], then click **Next** and **Finish**. 

	<img src="../Media/mobile-add-push-notifications-vs2013-3.png" />

	The mobile service is updated to register your app package SID and client secret and a new **channels** table is created. Mobile Services is now configured to work with Windows Push Notification Services (WNS) to be able to send notifications to your app.   

	<div class="dev-callout"><b>Note</b>
		<p>When your app isn't already configured to connect to the mobile service, the wizard also completes the same configuration tasks demonstrated in <strong>Get started with data</strong>.</p>
	</div>

<!-- URLs. -->
[Get started with Mobile Services]: /en-us/develop/mobile/tutorials/get-started/
[Get started with data]: /en-us/develop/mobile/tutorials/get-started-with-data-dotnet/
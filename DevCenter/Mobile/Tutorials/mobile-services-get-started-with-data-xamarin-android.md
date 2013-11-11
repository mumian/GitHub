<properties linkid="develop-mobile-tutorials-get-started-with-data-xamarin-android" urlDisplayName="Get Started with Data" pageTitle="Get started with data (Xamarin.Android) - Windows Azure Mobile Services" writer="rpeters" metaKeywords="Windows Azure Xamarin.Android data, Azure mobile services data" metaDescription="Learn how to store and access data from your Windows Azure Mobile Services Xamarin.Android app." metaCanonical="" disqusComments="1" umbracoNaviHide="1" />

<div chunk="../chunks/article-left-menu-xamarin-android.md" />

# Get started with data in Mobile Services
<div class="dev-center-tutorial-selector sublanding">    
	<a href="/en-us/develop/mobile/tutorials/get-started-with-data-dotnet" title="Windows Store C#">Windows Store C#</a><a href="/en-us/develop/mobile/tutorials/get-started-with-data-js" title="Windows Store JavaScript">Windows Store JavaScript</a><a href="/en-us/develop/mobile/tutorials/get-started-with-data-wp8" title="Windows Phone">Windows Phone</a><a href="/en-us/develop/mobile/tutorials/get-started-with-data-ios" title="iOS">iOS</a><a href="/en-us/develop/mobile/tutorials/get-started-with-data-android" title="Android">Android</a><a href="/en-us/develop/mobile/tutorials/get-started-with-data-html" title="HTML">HTML</a><a href="/en-us/develop/mobile/tutorials/get-started-with-data-xamarin-ios" title="Xamarin.iOS">iOS C#</a><a href="/en-us/develop/mobile/tutorials/get-started-with-data-xamarin-android" title="Xamarin.Android" class="current">Android C#</a>
</div>	


<div class="dev-onpage-video-clear clearfix">
<div class="dev-onpage-left-content">

<p>This topic shows you how to use Windows Azure Mobile Services to leverage data in a Xamarin.Android app. In this tutorial, you will download an app that stores data in memory, create a new mobile service, integrate the mobile service with the app, and then login to the Windows Azure Management Portal to view changes to data made when running the app.</p>

</div>
<div class="dev-onpage-video-wrapper"><a href="http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Android-Getting-Started-With-Data-Connecting-your-app-to-Windows-Azure-Mobile-Services" target="_blank" class="label">watch the tutorial</a> <a style="background-image: url('/media/devcenter/mobile/videos/mobile-android-get-started-data-180x120.png') !important;" href="http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Android-Getting-Started-With-Data-Connecting-your-app-to-Windows-Azure-Mobile-Services" target="_blank" class="dev-onpage-video"><span class="icon">Play Video</span></a><span class="time">15:32</span></div>
</div>

<div class="dev-callout"><b>Note</b>
<p>This tutorial is intended to help you better understand how Mobile Services enables you to use Windows Azure to store and retrieve data from a Xamarin.Android app. As such, this topic walks you through many of the steps that are completed for you in the Mobile Services quickstart. If this is your first experience with Mobile Services, consider first completing the tutorial <a href="/en-us/develop/mobile/tutorials/get-started-xamarin-android">Get started with Mobile Services</a>.</p>
</div>

This tutorial walks you through these basic steps:

1. [Download the Xamarin.Android app project][GitHub] 
2. [Create the mobile service]
3. [Add a data table for storage]
4. [Update the app to use Mobile Services]
5. [Test the app against Mobile Services]

<div class="dev-callout"><strong>Note</strong> <p>To complete this tutorial, you need a Windows Azure account. If you don't have an account, you can create a free trial account in just a couple of minutes. For details, see <a href="http://www.windowsazure.com/en-us/pricing/free-trial/?WT.mc_id=AED8DE357" target="_blank">Windows Azure Free Trial</a>.</p></div> 

This tutorial requires the [Azure Mobile Services Component], [Xamarin.Android], and Android SDK 4.2 or a later version. 

<div class="dev-callout"><b>Note</b>
<p>The downloaded GetStartedWithData project requires targetting Android 4.2 or a later version. However, the Mobile Services SDK requires only Android 2.2 or a later version.</p>
</div>

<h2><a name="download-app"></a><span class="short-header">Download the project</span>Download the GetStartedWithData project</h2>

This tutorial is built on the [GetStartedWithData app][GitHub], which is a Xamarin.Android app. The UI for this app is identical to the app generated by the Mobile Services Android quickstart, except that added items are stored locally in memory. 

1. Download the `GetStartedWithData` sample app and extract the files on your computer. 

2. In Xamarin Studio, click **File** then **Open**, browse to where you extracted the GetStartedWithData sample project, and select **XamarinTodoQuickStart.Android.sln** and open it.

3. Locate and open the **TodoActivity** class

   ![][12]

   Notice that there are `// TODO::` comments that specify the steps you must take to make this app work with your mobile service.

5. From the **Run** menu, click **Start Without Debugging**, you will then be asked to pick an emulator or attached USB Android device.

	<div class="dev-callout"><strong>Note</strong> <p>You can run this project using an Android phone, or using the Android emulator. Running with an Android phone  requires you to download a phone-specific USB driver.</p> <p>To run the project in the Android emulator, you must define a least one Android Virtual Device (AVD). Use the AVD Manager to create and manage these devices.</p></div>

6. In the app, type meaningful text, such as _Complete the tutorial_, and then click **Add**.

   ![][13]

   Notice that the saved text is stored in an in-memory collection and displayed in the list below.

<h2><a name="create-service"></a><span class="short-header">Create mobile service</span>Create a new mobile service in the Management Portal</h2>

<div chunk="../chunks/mobile-services-create-new-service-data.md" />

<h2><a name="add-table"></a><span class="short-header">Add a new table</span>Add a new table to the mobile service</h2>

To be able to store app data in the new mobile service, you must first create a new table.  

1. In the Management Portal, click **Mobile Services**, and then click the mobile service that you just created.

2. Click the **Data** tab, then click **+Create**.

   ![][5]

   This displays the **Create new table** dialog.

3. In **Table name** type _TodoItem_, then click the check button.

  	![][6]

  	This creates a new storage table **TodoItem** with the default permissions set, which means that any user of the app can access and change data in the table. 

    <div class="dev-callout"> 
	<b>Note</b> 
	<p>The same table name is used in Mobile Services quickstart. However, each table is created in a schema that is specific to a given mobile service. This is to prevent data collisions when multiple mobile services use the same database.</p> 
	</div>

4. Click the new **TodoItem** table and verify that there are no data rows.

5. Click the **Columns** tab and verify that there is only a single **id** column, which is automatically created for you.

  	This is the minimum requirement for a table in Mobile Services. 

    <div class="dev-callout"><b>Note</b>
	<p>When dynamic schema is enabled on your mobile service, new columns are created automatically when JSON objects are sent to the mobile service by an insert or update operation.</p>
    </div>

You are now ready to use the new mobile service as data storage for the app.

<h2><a name="update-app"></a><span class="short-header">Update the app</span>Update the app to use the mobile service for data access</h2>

Now that your mobile service is ready, you can update the app to store items in Mobile Services instead of the local collection. 

1. If you don't already have **Azure Mobile Services** listed in the Components folder, you can get it by right-clicking **Components**, choosing **Get More Components** and then searching for **Azure Mobile Services**.

  	This adds the Mobile Services SDK component to the project.

2. Open the **AndroidManifest.xml** file and ensure the following permission line exists:

		<uses-permission android:name="android.permission.INTERNET" />

  	This enables the app to access Mobile Services in Windows Azure.

3. From the **Solution** window, open the **TodoActivity** class, and uncomment the following line of code: 

		// using Microsoft.WindowsAzure.MobileServices;
 
4. We will remove the in-memory list currently used by the app, so we can replace it with a mobile service. In the **TodoActivity** class, comment out the following line of code, which defines the existing **todoItemList** list.

		public List<TodoItem> todoItemList = new ArrayList<TodoItem>();

5. Once the previous step is done, the project will indicate build errors. Search for the three remaining locations where the `todoItemList` variable is used and comment out the sections indicated. 

6. We now add our mobile service. Uncomment the following lines of code:

        // private MobileServiceClient client; // Mobile Service Client references

7. In the Management Portal, click **Mobile Services**, and then click the mobile service you just created.

8. Click the **Dashboard** tab and make a note of the **Site URL**, then click **Manage keys** and make a note of the **Application key**.

   ![][8]

  	You will need these values when accessing the mobile service from your app code.

9. In the **Constants** class, uncomment the following member variables:

        // public const string ApplicationURL = @"AppUrl";


11. In the **OnCreate** method, uncomment the following lines of code that define the **MobileServiceClient** variable:


  	This creates a new instance of MobileServiceClient that is used to access your mobile service. It also creates the MobileServiceTable instance that is used to proxy data storage in the mobile service.

12. Find the ProgressFilter class at the bottom of the file and uncomment it. This class displays a 'loading' indicator while MobileServiceClient is running network operations.

13. Uncommment these lines of the **CheckItem** method:

        /*

   	This sends an item update to the mobile service and removes checked items from the adapter.
    
15. Uncommment these lines of the **AddItem** method:
	
        /*

  	This code creates a new item and inserts it into the table in the remote mobile service.

16. Uncommment these lines of the **RefreshItemsFromTableAsync** method:

        /*

	This queries the mobile service and returns all items that are not marked as complete. Items are added to the adapter for binding.
		

Now that the app has been updated to use Mobile Services for backend storage, it's time to test the app against Mobile Services.

<h2><a name="test-app"></a><span class="short-header">Test the app</span>Test the app against your new mobile service</h2>

1. From the **Run** menu, click **Start Without Debugging** to start the project. You will be asked to pick an existing emulator image or an attached USB Android device.

	This executes your app, built with Xamarin.Android, that uses the client library to send a query that returns items from your mobile service.

5. As before, type meaningful text, then click **Add**.

   This sends a new item as an insert to the mobile service.

3. In the [Management Portal], click **Mobile Services**, and then click your mobile service.

4. Click the **Data** tab, then click **Browse**.

   ![][9]
  
   Notice that the **TodoItem** table now contains data, with id values generated by Mobile Services, and that columns have been automatically added to the table to match the TodoItem class in the app.

This concludes the **Get started with data** tutorial for Xamarin.Android.

## Get completed example
Download the [completed example project]. Be sure to update the **applicationURL** and **applicationKey** variables with your own Azure settings. 

## <a name="next-steps"> </a>Next steps

This tutorial demonstrated the basics of enabling a Xamarin.Android app to work with data in Mobile Services. 

Next, consider completing one of the following tutorials that is based on the GetStartedWithData app that you created in this tutorial:

* [Validate and modify data with scripts]
  <br/>Learn more about using server scripts in Mobile Services to validate and change data sent from your app.

* [Refine queries with paging]
  <br/>Learn how to use paging in queries to control the amount of data handled in a single request.

Once you have completed the data series, try these other Xamarin.Android tutorials:

* [Get started with authentication] 
	<br/>Learn how to authenticate users of your app.

* [Get started with push notifications] 
  <br/>Learn how to send a very basic push notification to your app with Mobile Services.

<!-- Anchors. -->

[Get the Windows Store app]: #download-app
[Create the mobile service]: #create-service
[Add a data table for storage]: #add-table
[Update the app to use Mobile Services]: #update-app
[Test the app against Mobile Services]: #test-app
[Next Steps]:#next-steps

<!-- Images. -->
[0]: ../Media/mobile-quickstart-startup-android.png
[1]: ../../Shared/Media/plus-new.png
[2]: ../Media/mobile-create.png
[3]: ../Media/mobile-create-page1.png
[4]: ../Media/mobile-create-page2.png
[5]: ../Media/mobile-data-tab-empty.png
[6]: ../Media/mobile-create-todoitem-table.png
[8]: ../Media/mobile-dashboard-tab.png
[9]: ../Media/mobile-todoitem-data-browse.png
[10]: ../Media/mobile-data-sample-download-android.png
[12]: ../Media/mobile-eclipse-project.png
[13]: ../Media/mobile-quickstart-startup-android.png

<!-- URLs. TODO:: update 'Download the Android app project' download link, 'GitHub', completed project, etc. -->
[Validate and modify data with scripts]: ./mobile-services-validate-and-modify-data-dotnet.md
[Refine queries with paging]: ./mobile-services-paging-data-xamarin-android.md
[Get started with Mobile Services]: ./mobile-services-get-started-xamarin-android.md
[Get started with data]: ./mobile-services-get-started-with-data-xamarin-android.md
[Get started with authentication]: ./mobile-services-get-started-with-users-xamarin-android.md
[Get started with push notifications]: ./mobile-services-get-started-with-push-xamarin-android.md
[WindowsAzure.com]: http://www.windowsazure.com/
[Windows Azure Management Portal]: https://manage.windowsazure.com/
[Management Portal]: https://manage.windowsazure.com/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[Download the Android app project]: http://www.google.com/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkID=282122
[Android SDK]: https://go.microsoft.com/fwLink/p/?LinkID=280125
[Xamarin.Android]: http://xamarin.com/download
[completed example project]: http://www.google.com
# OneSignalSample
Contoh Push Notification menggunakan OneSignal

# Requirements
		GCM Project ID and Server Api Key ( dari Firebase )
		Akun One Signal
    
# Android Project
1. masuk ke struktur project app/build.gradle dan tulis kode dibawah dependency

		compile 'com.google.android.gms:play-services:8.1.0'
		compile 'com.google.android.gms:play-services-ads:8.1.0'
		compile 'com.google.android.gms:play-services-identity:8.1.0'
		compile 'com.google.android.gms:play-services-gcm:8.1.0'
		compile 'com.onesignal:OneSignal:2.+@aar'
		compile 'com.google.android.gms:play-services-analytics:8.1.0'
		compile 'com.google.android.gms:play-services-location:8.1.0'	
		
2. kemudian defaultconfig dibawah VersionName tambahkan

			manifestPlaceholders = [manifestApplicationId: "${applicationId}",
						onesignal_app_id: "OneSignal App ID",
						onesignal_google_project_number: "GCM Project ID"]

3. masuk ke Mainfile aplikasi(MainActivity) lalu tambahkan kode dibawah method below super.onCreate();

			OneSignal.startInit(this)
				.setNotificationOpenedHandler(new ExampleNotificationOpenedHandler())
				.init();

4. kemudian tambahkan method baru

			private class ExampleNotificationOpenedHandler implements OneSignal.NotificationOpenedHandler {
			    @Override
			    public void notificationOpened(String message, JSONObject additionalData, boolean isActive) {
				try {
				    if (additionalData != null) {
					if (additionalData.has("actionSelected"))
					    Log.d("OneSignalExample", "OneSignal notification button with id " + additionalData.getString("actionSelected") + " pressed");

                        Log.d("OneSignalExample", "Full additionalData:\n" + additionalData.toString());
                    	}
			} catch (Throwable t) {
			    t.printStackTrace();
			}		
			
selesai, tinggal setting di OneSignal saja.. selamat berkarya :)		

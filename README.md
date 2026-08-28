
# Ex.No:4 Create Your Own Content Providers to get Contacts details.


## AIM:

To create your own content providers to get contacts details using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Latest Version)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as “contentprovider″ and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Get contacts details and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the contact name and phone number using content providers.
Developed by: KAVIBHARATHI K
Registeration Number : 212224220045
*/
```
### AndroidManifist.xml
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">
<uses-permission android:name="android.permission.READ_CONTACTS" />
    <uses-permission android:name="android.permission.WRITE_CONTACTS" />

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.ContentProvider">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```
### MainActivity.java
```
package com.example.contentprovider;

import android.Manifest;
import android.content.ContentResolver;
import android.content.pm.PackageManager;
import android.database.Cursor;
import android.net.Uri;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.util.Log;
import android.view.View;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

public class MainActivity extends AppCompatActivity
{

    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);
    }
    public void btnGetContactPressed(View v)
    {
        getPhoneContacts();
    }

    public void getPhoneContacts()
    {
        if(ContextCompat.checkSelfPermission(this , Manifest.permission.READ_CONTACTS) != PackageManager.PERMISSION_GRANTED)
        {
            ActivityCompat.requestPermissions(this , new String[] {Manifest.permission.READ_CONTACTS} , 1);
            return;
        }

        ContentResolver contentResolver = getContentResolver();
        Uri uri = ContactsContract.CommonDataKinds.Phone.CONTENT_URI;
        try (Cursor cursor = contentResolver.query(uri, null, null, null, null))
        {
            if (cursor != null && cursor.getCount() > 0)
            {
                Log.i("CONTACT_PROVIDER_DEMO",
                        "TOTAL # of Contacts ::: " + cursor.getCount());

                while (cursor.moveToNext())
                {
                    String contactName = cursor.getString(
                            cursor.getColumnIndexOrThrow(ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME));
                    String contactNumber = cursor.getString(
                            cursor.getColumnIndexOrThrow(ContactsContract.CommonDataKinds.Phone.NUMBER));

                    Log.i("CONTACT_PROVIDER_DEMO",
                            "Contact Name ::: " + contactName + " Contact Number ::: " + contactNumber);
                }
            }
            else
            {
                Log.e("CONTACT_PROVIDER_DEMO", "No contacts found or cursor is null");
            }
        }
    }
}
```
### activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/button"
        android:layout_width="153dp"
        android:layout_height="65dp"
        android:onClick="btnGetContactPressed"
        android:text="Get Contacts"
        android:textColorLink="#000000"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.459" />

    <TextView
        android:id="@+id/textView"
        android:layout_width="173dp"
        android:layout_height="31dp"
        android:fontFamily="sans-serif-medium"
        android:text="ContentProvider"
        android:textColor="#6851A5"
        android:textSize="24sp"
        android:typeface="serif"
        app:layout_constraintBottom_toTopOf="@+id/button"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.779" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
## OUTPUT
### MainActivity.java
<img width="1919" height="1139" alt="image" src="https://github.com/user-attachments/assets/1635be78-4ac0-4fd0-bfe1-22703189f55f" />
### AndroidManifist.xml
<img width="1917" height="1137" alt="image" src="https://github.com/user-attachments/assets/61fafeb2-1f7a-48ab-956f-a55da8c574a2" />
### activity_main.xml
<img width="1919" height="1136" alt="image" src="https://github.com/user-attachments/assets/646b6b67-07e0-4296-9fae-8d3852350be7" />
### ContentProvider App
<img width="449" height="795" alt="image" src="https://github.com/user-attachments/assets/eccfae1f-5b3b-4909-b3c1-2cb5932b1e97" />
### Contacts from Mobile Via LogCat
<img width="1916" height="1146" alt="image" src="https://github.com/user-attachments/assets/c52e8811-5d65-4520-800a-5dbbf3f08953" />




## RESULT
Thus a Simple Android Application create your own content providers to get contacts details using Android Studio is developed and executed successfully.



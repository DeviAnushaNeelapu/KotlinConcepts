# SharedPreferences 
<img src="https://user-images.githubusercontent.com/46557268/131819997-45376b37-98fb-4394-8861-9ba8f2fc6f67.png"  />

###  Shared preferences allows to store data in form of XML Key Pair value. Where the value will be stored basis of key. Similar key will be used to access the value.

### It will always store latest value.


<img src="https://user-images.githubusercontent.com/46557268/131818472-537ed23b-1ad6-48c7-bca1-98e435ed3180.jpeg" width="200" height="300" align="center"/>



## activity_main
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="20dp"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="16dp"
        android:layout_marginTop="32dp"
        android:layout_marginEnd="16dp"
        android:text="Registration Page"
        android:textColor="@color/purple_500"
        android:textSize="24sp"
        android:textStyle="bold"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <EditText
        android:layout_marginTop="32dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="enter name"
        android:id="@+id/name"
        android:inputType="textPersonName"
        />
    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="enter age"
        android:inputType="number"
        android:id="@+id/age"/>
    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="enter address"
        android:id="@+id/address"
        android:inputType="textPostalAddress"/>
    <Button
        android:id="@+id/submit"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="submit"/>
</LinearLayout>
```
# mainactivity.kt
```
package com.example.sharedprefernces

import android.content.Context
import android.content.SharedPreferences
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.EditText

class MainActivity : AppCompatActivity() {
    var nameED : EditText? = null
    var ageED: EditText? = null
    var addressED: EditText? = null

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }
    override fun onStart() {
        super.onStart()

        nameED = findViewById(R.id.name);
        ageED = findViewById(R.id.age)
        addressED = findViewById(R.id.address)
    }

    //Procedure to save data withing Preferences
    override fun onPause() {
        super.onPause()

        //1: Create a Shared Preferences Object
        val sharedPreferences : SharedPreferences = this.getSharedPreferences("myPrefs", Context.MODE_PRIVATE)

        //2: Create and SharedPreferences Editor to edit the file.
        val editor : SharedPreferences.Editor = sharedPreferences.edit()

        //3.Add the data
        editor.putString("nameKey",nameED!!.text.toString())
        editor.putString("ageKey",ageED!!.text.toString())
        editor.putString("addressKey",addressED!!.text.toString())

        //4: Save Operation
        editor.apply()
    }

    override fun onResume() {
        super.onResume()

        //1: Create a Shared Preferences Object
        val sharedPreferences :SharedPreferences = this.getSharedPreferences("myPrefs", Context.MODE_PRIVATE)

        //2: Reterive the value
        val nameValue = sharedPreferences.getString("nameKey",null)
        val ageValue = sharedPreferences.getString("ageKey",null)
        val addressValue = sharedPreferences.getString("addressKey",null)

        //3:Check the value
        if(nameValue != null && ageValue!= null && addressValue!= null){
            //3.1 Update the value with Edit Text US component

            nameED!!.setText(nameValue.toString())
            ageED!!.setText(ageValue.toString())
            addressED!!.setText(addressValue.toString())
        }

    }
}



```

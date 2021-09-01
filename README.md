# RecyclerView_Kotlin
## Display large sets of data in your UI while minimizing memory usage.
### Dependencies of recyclerview 
 ``` 
 dependencies {
    implementation("androidx.recyclerview:recyclerview:1.2.1")
    // For control over item selection of both touch and mouse driven selection
    implementation("androidx.recyclerview:recyclerview-selection:1.1.0")
}
```
![WhatsApp Image 2021-09-01 at 2 19 07 PM](https://user-images.githubusercontent.com/46557268/131645068-b5174b4f-eb50-4106-9ec3-80cb60cdf5a9.jpeg)
![WhatsApp Image 2021-09-01 at 2 19 06 PM](https://user-images.githubusercontent.com/46557268/131645117-77ca7bf8-5144-4e4d-9f4f-a99beeff0baa.jpeg)

### activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/myrec"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="8dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
### recycler_row_layout.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <ImageView
        android:id="@+id/productImageView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="8dp"
        android:layout_marginLeft="8dp"
        android:layout_marginTop="8dp"
        android:layout_marginBottom="8dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:srcCompat="@tools:sample/avatars" />

    <TextView
        android:id="@+id/productNameTV"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="24dp"
        android:layout_marginLeft="24dp"
        android:layout_marginTop="10dp"
        android:layout_marginEnd="16dp"
        android:layout_marginRight="16dp"
        android:text="Product Name"
        android:textColor="@color/black"
        android:textSize="18sp"
        android:textStyle="bold"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/productImageView"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/productPriceTV"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="24dp"
        android:layout_marginLeft="24dp"
        android:layout_marginTop="32dp"
        android:layout_marginEnd="16dp"
        android:layout_marginRight="16dp"
        android:text="Product Price"
        android:textColor="@color/black"
        android:textStyle="bold"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/productImageView"
        app:layout_constraintTop_toBottomOf="@+id/productNameTV" />

    <TextView
        android:id="@+id/productCountryTV"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="24dp"
        android:layout_marginLeft="24dp"
        android:layout_marginTop="32dp"
        android:layout_marginEnd="16dp"
        android:layout_marginRight="16dp"
        android:layout_marginBottom="8dp"
        android:text="Product Made"
        android:textColor="@color/black"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/productImageView"
        app:layout_constraintTop_toBottomOf="@+id/productPriceTV" />

</androidx.constraintlayout.widget.ConstraintLayout>
```
### Mainactivity.kt
```
package com.example.navigations

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import androidx.recyclerview.widget.DividerItemDecoration
import androidx.recyclerview.widget.LinearLayoutManager
import androidx.recyclerview.widget.RecyclerView

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

    //Linking of Recycler View
    var myRecyclerView : RecyclerView = findViewById(R.id.myrec)

    myRecyclerView.adapter = MyAdapter()
    myRecyclerView.layoutManager = LinearLayoutManager(this)
    myRecyclerView.addItemDecoration(DividerItemDecoration(this,LinearLayoutManager.VERTICAL))
}

}
````

### MyAdapter.kt
``` 
package com.example.navigations

import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.ImageView
import android.widget.TextView
import androidx.recyclerview.widget.RecyclerView

class MyAdapter : RecyclerView.Adapter<MyAdapter.ViewHolder>() {

    //Step1: Prepare Data
    val productNameList = listOf<String>("Cartoon1","Cartoon2","Cartoon3","Cartoon4","Anusha","Nithya")
    val productPriceList = listOf<Int>(100,310,21,41,30,10)
    val productCountryList = listOf<String>("India","USA","UK","Germany","India","Vijaywada")


    //It will link the UI Component(RecyclerView Row) with Adapter using findViewBYId
    class ViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
        var productIV: ImageView
        var productName: TextView
        var productPrice: TextView
        var productCountry: TextView


        init {
            productIV = itemView.findViewById(R.id.productImageView)
            productName = itemView.findViewById(R.id.productNameTV)
            productPrice = itemView.findViewById(R.id.productPriceTV)
            productCountry = itemView.findViewById(R.id.productCountryTV)
        }
    }

    //It will Link with Layout ( RecyclerView Row)
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): MyAdapter.ViewHolder {
        val recycler_row_view = LayoutInflater.from(parent.context).inflate(R.layout.recycler_row_layout,parent,false)
        return ViewHolder(recycler_row_view)
    }

    //IT will link data with UI Component ( RecyclerView Row)
    override fun onBindViewHolder(holder: MyAdapter.ViewHolder, position: Int) {
        holder.productName.text = "Name: ${productNameList[position]}"
        holder.productPrice.text ="Price: ${productPriceList[position]} INR"
        holder.productCountry.text = "Made: ${productCountryList[position]}"
    }

    //Size of Data
    override fun getItemCount(): Int {
        return productCountryList.size
    }
}
```

# 1. 리스트
```kotlin
//list
var numlist: List<Int> = listOf(1,2,3,4,5)
val books = mutableListOf<String>() // 변경가능 리스트
for(number in numblist) println("$number ")
books.add("Python")
```

# 2. RecyclerView
RecyclerView : itemView집합 : itemdata집합
### 1) MainActivity.kt
```kotlin
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.View
import android.widget.Button
import android.widget.ImageView
import android.widget.TextView
import android.widget.Toast
import androidx.recyclerview.widget.RecyclerView

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val dataSet = DataSet().makeSet()
        val recyclerView = findViewById<RecyclerView>(R.id.recycler_view)
        recyclerView.adapter = ItemAdapter(this, dataSet)
        }
}
```
### 2) Affirmation
```kotlin
package com.example.firstapp

class Affirmation(var strResource: Int, val imageResource: Int)
```

### 3) DataSet
```kotlin
package com.example.firstapp

class DataSet {
    fun makeSet(): List<Affirmation> {
        return listOf<Affirmation>(Affirmation(R.string.affirmation1, R.drawable.image1),
            Affirmation(R.string.affirmation2, R.drawable.image2))
    }
}
```

### 4) ItemAdapter
```kotlin
package com.example.firstapp

import android.content.Context
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.ImageView
import android.widget.TextView
import androidx.recyclerview.widget.RecyclerView

class ItemAdapter(private val context: Context, private val dataSet: List<Affirmation>)
    :RecyclerView.Adapter<ItemAdapter.ItemViewHolder>() {
    class ItemViewHolder(private val view: View): RecyclerView.ViewHolder(view){
        val textview : TextView = view.findViewById(R.id.item_title)
        val imageview : ImageView = view.findViewById(R.id.item_image)
    }
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ItemViewHolder {
        // ItemViewHolder 객체를 만들어줌
        val item_layout = LayoutInflater.from(parent.context).inflate(R.layout.list_item, parent, false)
        return ItemViewHolder(item_layout)
    }

    override fun onBindViewHolder(holder: ItemViewHolder, position: Int) {
        // ViewHolder 만들어진곳에 데이터를 결합
        val item = dataset[position]
        holder.textview.text = context.resources.getString(item.strResource)
        holder.imageview.setImageResource(item.imageResource)
    }
    // 앞으로 처리해야할 데이터가 몇개
    override fun getItemCount() = dataset.size
}
```


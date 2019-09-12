# Android-Kotlin-Fragment
วิธีการทำ Fragment ในแอพแอนดรอยด์ด้วยภาษา Kotlin
ก่อนอื่นขออ้างอิงค์ถึงโค้ดอีกชุดหนึ่งก่อนครับ โดยให้ไปตั้งต้นจากโค้ดชุดนั้นก่อนนะครับ <a href="https://github.com/thavirat/Navigation">วิธีการทำ Navigation ในแอพแอนดรอยด์โดย Kotlin</a>
เมื่อได้โค้ดมาแล้วอย่างแรกที่เราต้องทำก็คือให้ทำการ สร้างฟังก์ชั่นสำหรับเปิด Fragment ขึ้นมาก่อนในไฟล์ MainActivity

```
fun openFragment(fragment: Fragment) {
    val transaction = supportFragmentManager.beginTransaction()
    transaction.replace(R.id.container, fragment)
    transaction.addToBackStack(null)
    transaction.commit()
}
```
และทำการแก้ไขฟังก์ชั่น onNavigationItemSelected ให้ไปเรียกใช้คำสั่งเปิด Fragment โดยตัวอย่างจะทำเพียงแค่หน้าแรกหน้าเดียว
โค้ดเดิม
```
R.id.nav_item_one -> Toast.makeText(this, "Clicked item one", Toast.LENGTH_SHORT).show()
```
โค้ดใหม่
```
R.id.nav_item_one -> {
    val homeFragment = FirstFragment.newInstance()
    openFragment(homeFragment)
    drawer.closeDrawer(GravityCompat.START)
}
```
และเพิ่มคำสั่งให้ทำการปิด Navigation เมื่อทำการกดเลือกเมนู โดยให้เพิ่มไปที่ฟังก์ชั่น onNavigationItemSelected นำคำสั่งไปไว้ก่อน return
```
drawer.closeDrawer(GravityCompat.START)
```
สรุปหน้าตาโค้ดจะได้ออกมาเป็นลักษณะดังนี้
<p align="center">
  <img src="https://tgf-programing.com/uploads/temp//1568306768-YhJGQ.jpg">
</p>

หลังจากนั้นให้ทำการสร้าง Fragment โดยให้คลิ๊กขวาเลือกที่ com.excample.{project} > New > Kotlin File/Class จากนั้นตั้งชื่อไฟล์ว่า FirstFragment และกด Enter
<p align="center">
  <img src="https://tgf-programing.com/uploads/temp//1568306728-HOYWV.jpg">
</p>
แล้วนำโค้ดชุดนี้ไปวาง
```
class FirstFragment : Fragment(){
    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View? {
        val rootView = inflater.inflate(R.layout.fragment_first_page, container, false)
        return rootView
    }

    companion object {
        fun newInstance(): FirstFragment {
            val fragment = FirstFragment()
            return fragment
        }
    }
}
```
จะได้หน้าตาเป็นแบบนี้
<p align="center">
  <img src="https://tgf-programing.com/uploads/temp//1568306871-EfTf6.jpg">
</p>

จากนั้นทำการสร้างไฟล์ fragment_first_page ในโฟลเดอร์ res > layout โดยคลิ๊กขวา แล้วเลือก New > Layout resource file และตั้งชื่อว่า fragment_first_page
และนำโค้ดชุดนี้ไปวาง สำหรับใครที่ไม่สามารถวางโค้ดได้ให้เลือกโหมดมุมซ้ายล่างเป็นโหมด Text ก่อน
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    >

    <TextView
        android:id="@+id/textView2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Firstpage"
        android:textSize="36sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>

จะได้โค้ดหน้าตาออกมาเป็นดังนี้
<p align="center">
  <img src="https://tgf-programing.com/uploads/temp//1568307111-RXzXH.jpg">
</p>
และสุดท้ายให้แก้ไขไฟล์ activity_main โดยเพิ่มโค้ดชุดนี้ลงไป
```
<FrameLayout
        android:id="@+id/container"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_behavior="@string/appbar_scrolling_view_behavior" android:paddingTop="30dp"/>
```
<p align="center">
  <img src="https://tgf-programing.com/uploads/temp//1568307216-XvSFi.jpg">
</p>

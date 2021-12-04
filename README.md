Project aplikasi ini merupakan aplikasi untuk menampilkan jam saat ini. Jam dapat diubah dalam 2 mode, yaitu mode am pm dan mode 24-hour.
public class MainActivity extends AppCompatActivity {
   TextView jam; //textiew untuk menampilkan jam
   Button mode1,mode2; //mode1 untuk mode 24-hour button dan mode2 untuk am pm button
   int mode = 0; //mode diawali dengan mode 0 yaitu 24-hour
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);
       jam = findViewById(R.id.jam); //binding xml dengan java
       mode1 = findViewById(R.id.mode1);//binding xml dengan java
       mode2 = findViewById(R.id.mode2);//binding xml dengan java
       mode1.setOnClickListener(view->{ //buat listener pada button mode1
           mode = 0; //buat mode menjadi 0 jika diklik
       });
       mode2.setOnClickListener(view->{//buat listener pada button mode2
           mode = 1;//buat mode menjadi 1 jika di klik
       });
       runTimer(); //panggil method runTimer
   }
   private void runTimer() //private method runTimer
   {
       final Handler handler = new Handler(); //handler untuk thread
       handler.post(new Runnable() { //jalankan handler
           @Override
           public void run() //method yang dijalankan thread
           {
               if(mode == 0) { //kalau mode 0
                   //settext waktu saat ini dalam format 24-hours
                   jam.setText(new SimpleDateFormat("HH:mm:ss", Locale.getDefault()).format(new Date()));
               }else{
                   //settext waktu saat ini dalam format am pm
                   jam.setText(new SimpleDateFormat("HH:mm:ss aa", Locale.getDefault()).format(new Date()));
               }
               //tahan thread 1 detik sesuai dengan update waktu setiap 1 detik berubah
               handler.postDelayed(this, 1000);
           }
       });
   }
}

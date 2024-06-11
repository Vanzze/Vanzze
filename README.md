Desktop Application
1. Buat project Windows Forms App (.NET Framework)
2. Install EntityFramework di Tools > NuGet Package Manager > Manage NuGet Packages For Solution > Search Entity Framework
3. Masuk di SQLServer > Connect Server 
4. New Database > New Table
5. Sesuaikan table dengan soal, 
	id set ke primary key int, dan set Identity Specification Yes "1",
	jika data hanya angka int,
	jika huruf nvarchar(255)
6. Buat Model Entity, di Add > New Item > Data > ADO.Net
7. Pilih EF Designer from database > New Connection 
8. Sesuaikan Server Name dengan SQL Server, contoh: joaquin\SQLEXPRESS01 > Trust Server Certificate centang
9. Pilih database yg telah dibuat > Next > Add semua table > Finish
10. Buat Form sesuai soal
11. Validasi textbox dengan if-else
12. Jika ada table yang baru dibuat, untuk mengupdate di modelnya dengan cara > NamaModel.edmx lalu klik kanan di layer > Update Model from database
13. Update NamaModel.tt dengan > Klik kana > Debug T4 Template
14. Buat entities di setiap form = contohEntities entities = new contohEntities();
14. Validasi role saat login menggunakan if-else, cari dulu user nya, jika ketemu 
	contoh: if(user.role == "admin") {
			new FormAdmin().Show()
			this.Hide()
		else() {
			new FormUser().Show()
			this.Hide()
		}
15. CRUD Data
	- Create: 
		 var user = new user();
		 user.email = txtEmail.Text;
		 user.password = txtPass.Text;
 		entities.users.Add(user);
 		entities.SaveChanges();
	- Read :
		Select All:
		 var users = entities.users.Select(u => u);
		 dataGridView1.DataSource = users.ToList();	
		Select By Id;
		var user = entities.users.FirstOrDefault(u => u.Id == id);

		if (user != null)
		{
   			 /blablaba
		} else { blablala }
	- Update: Cari dulu, lalu saveChanges
	- Delete: Cari dulu, baru delete
		entities.users.Remove(user);
                entities.SaveChanges();
16. Searching and filtering = jika filter gunakan where
				contoh   query = query.Where(u => u.email.Contains(emailToSearch));
17. Join table = relationship
18. Aggregate query = angka angka seperti max min average, contoh di chatgpt
19. Display data chart = https://youtu.be/1HBMrDFZGOI?si=Se4mH-92vocmC-fY


API
1. Buat project Laravel dengan composer create-project laravel/laravel nama-app
2. Buat database di laragon, connect 
3. Ubah .env sesuai dengan nama database
4. install routes api dengan php artisan install:api
5. hapus migration table kecuali users , kemudian php artisan migrate
6. untuk refresh , php artisan migrate:fresh
7. buat controller dan model, php artisan make:controller NamaController, php artisan make:model NamaModel
8. buat table migrate = php artisan make:migration create_nama_table > php artisan migrate
9. jika sudah lengkap "controller, model, migration", tambahkan 
	protected $table = "namatable"
	protected $guarded = []
10. buat public function di controller
11. daftarkan di routes/api
12. php artisan ser untuk menjalankan
13. Join Query = relation, has many dan belongs to, seperti kemarin Category hasMany Product, Product belongsTo Category, untuk get gunakan with,contoh Category::with("product)->get();
14. Aggregate Query = min, max, avg, lihat contoh di chatgpt
15. searching = gunakan where
public function searchProducts(Request $request)
{
    $searchTerm = $request->input('search'); // Mengambil input pencarian dari request
    $products = Product::where('name', 'LIKE', '%' . $searchTerm . '%')->get();

    return response()->json($products, 200)

	url untuk search, contoh: http://127.0.0.1/products?minyak pakai "?"
}
16. jika error 400, 404

Mobile App
1. Buat project android studio > Empty Views Activity
2. build-gradle tambahkan 
	   buildFeatures {
     		   viewBinding true
    		}

	kemudian implementation yang diperlukan
	seperti   implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-core:1.7.3'
    implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.3'
    implementation 'androidx.lifecycle:lifecycle-runtime-ktx:2.6.2'
3. Gradle Sync Now
3. tambahkan di res > xml > buat network.xml > 
	<?xml version="1.0" encoding="utf-8"?>
	<network-security-config>
    		domain-config cleartextTrafficPermitted="true">
        		domain includeSubdomains="true">10.0.2.2</domain>
   		</domain-config>
	</network-security-config>
4. tambahkan AndroidManifest >     <uses-permission android:name="android.permission.INTERNET" /> >  android:networkSecurityConfig="@xml/network"
5. Ubah di setiap activity
	 private lateinit var binding: ActivityNameBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityNameBinding.inflate(layoutInflater)
        setContentView(binding.root)
6. Buat data model, menggunakan Json To Kotlin
7. GET, POST, PUT, DELETE, sesuaikan dengan API
8. Untuk menampilkan banyak data menggunakan,RecyclerView

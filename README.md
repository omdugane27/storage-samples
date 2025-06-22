plugins {
    id 'com.android.application'
    id 'com.google.gms.google-services'
}

android {
    compileSdk 33
    defaultConfig {
        applicationId "com.example.instaclone"
        minSdk 21
        targetSdk 33
        versionCode 1
        versionName "1.0"
    }
}

dependencies {
    implementation 'com.google.firebase:firebase-auth:22.0.0'
    implementation 'com.google.firebase:firebase-firestore:24.7.1'
    implementation 'com.google.firebase:firebase-storage:20.3.0'
    implementation 'com.github.bumptech.glide:glide:4.12.0'
    implementation 'androidx.recyclerview:recyclerview:1.2.1'
}
override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
    super.onActivityResult(requestCode, resultCode, data)
    if (requestCode == OPEN_DIRECTORY_REQUEST_CODE) {
        if (resultCode == Activity.RESULT_OK) {
            val directoryUri = data?.data ?: return
            // Open with `DocumentFile.fromTreeUri`...
        } else {
            // The user cancelled the request.
        }
    }
}class LoginActivity : AppCompatActivity() {
    private lateinit var auth: FirebaseAuth
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_login)
        auth = FirebaseAuth.getInstance()

        findViewById<Button>(R.id.loginBtn).setOnClickListener {
            val email = findViewById<EditText>(R.id.emailEt).text.toString()
            val password = findViewById<EditText>(R.id.passwordEt).text.toString()

            auth.signInWithEmailAndPassword(email, password)
                .addOnSuccessListener {
                    startActivity(Intent(this, MainActivity::class.java))
                }
        }

        findViewById<Button>(R.id.signupBtn).setOnClickListener {
            val email = findViewById<EditText>(R.id.emailEt).text.toString()
            val password = findViewById<EditText>(R.id.passwordEt).text.toString()

            auth.createUserWithEmailAndPassword(email, password)
                .addOnSuccessListener {
                    Toast.makeText(this, "Signup Success!", Toast.LENGTH_SHORT).show()
                }
        }
    }
}

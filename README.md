# hi


To design a two-page Android application layout for the Freshers' Party registration at Graphic Era University for the MCA III semester, the application will provide an intuitive interface for volunteer registration and participation status viewing. Page 1 will function as the Volunteer Registration Form, allowing users to input details such as the volunteer's name, student ID, department, contact information, and contribution fund amount. Below the input fields, there will be a section displaying the names and contributions of registered volunteers in a static format. A Submit Button will allow users to complete the registration process. Page 2 will present the Participation Status, titled "Freshers' Party Participation Status." This page will include two separate sections: one displaying the names of students who are actively participating and another for those who are not interested in the event.


Java Code (MainActivity.java and StatusActivity.java)
MainActivity.java (for Registration Form)

```
package com.example.freshersparty;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private EditText nameField, studentIdField, departmentField, contactField, fundField;
    private Button submitButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Initialize input fields
        nameField = findViewById(R.id.nameField);
        studentIdField = findViewById(R.id.studentIdField);
        departmentField = findViewById(R.id.departmentField);
        contactField = findViewById(R.id.contactField);
        fundField = findViewById(R.id.fundField);

        // Initialize the submit button
        submitButton = findViewById(R.id.submitButton);

        // On submit button click
        submitButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // Get input values
                String name = nameField.getText().toString();
                String studentId = studentIdField.getText().toString();
                String department = departmentField.getText().toString();
                String contact = contactField.getText().toString();
                String fund = fundField.getText().toString();

                // Pass the data to StatusActivity using Intent
                Intent intent = new Intent(MainActivity.this, StatusActivity.class);
                intent.putExtra("name", name);
                intent.putExtra("studentId", studentId);
                intent.putExtra("department", department);
                intent.putExtra("contact", contact);
                intent.putExtra("fund", fund);
                startActivity(intent);
            }
        });
    }
}

```


StatusActivity.java (for Participation Status)

```
package com.example.freshersparty;

import android.os.Bundle;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

public class StatusActivity extends AppCompatActivity {

    private TextView activeParticipantsText, notInterestedText;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_status);

        // Initialize TextView fields
        activeParticipantsText = findViewById(R.id.activeParticipantsText);
        notInterestedText = findViewById(R.id.notInterestedText);

        // Retrieve data from Intent
        String name = getIntent().getStringExtra("name");
        String studentId = getIntent().getStringExtra("studentId");
        String department = getIntent().getStringExtra("department");
        String contact = getIntent().getStringExtra("contact");
        String fund = getIntent().getStringExtra("fund");

        // Display the participation status based on the retrieved data
        activeParticipantsText.setText("Active Participants:\n" + name + " (" + studentId + ") - Dept: " + department + "\nContribution: ₹" + fund);
        notInterestedText.setText("Not Interested Participants: None");  // You can update this dynamically later
    }
}

```

XML Layout Files
activity_main.xml (for Registration Form)
```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <EditText
        android:id="@+id/nameField"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Volunteer Name" />

    <EditText
        android:id="@+id/studentIdField"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Student ID" />

    <EditText
        android:id="@+id/departmentField"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Department" />

    <EditText
        android:id="@+id/contactField"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Contact Information" />

    <EditText
        android:id="@+id/fundField"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Contribution Fund (₹)" />

    <Button
        android:id="@+id/submitButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Submit" />
</LinearLayout>

```


activity_status.xml (for Participation Status)


```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:id="@+id/activeParticipantsText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Active Participants:" />

    <TextView
        android:id="@+id/notInterestedText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Not Interested Participants:" />
</LinearLayout>

```

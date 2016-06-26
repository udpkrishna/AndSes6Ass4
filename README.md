# AndSes6Ass4

Main Activity.java
package me.rk.andses6ass4;

import android.content.Intent;
import android.net.Uri;
import android.provider.ContactsContract;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.ContextMenu;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    private Button mContextButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mContextButton=(Button) findViewById(R.id.contextButton);
        registerForContextMenu(mContextButton);
        mContextButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                openContextMenu(v);
            }
        });
    }

    @Override
    public void onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo) {
        super.onCreateContextMenu(menu,v,menuInfo);
        menu.add(0,0,0,"Call");
        menu.add(0,1,0,"SMS");

    }

    @Override
    public boolean onContextItemSelected(MenuItem item) {
        if (item.getTitle()=="Call"){
            Intent contactintent= new Intent();
            contactintent.setAction(Intent.ACTION_VIEW);
            contactintent.setData(ContactsContract.Contacts.CONTENT_URI);
            startActivity(contactintent);
            return true;
        }else if (item.getTitle()=="SMS"){
            Toast.makeText(MainActivity.this, "In SMS", Toast.LENGTH_SHORT).show();
            Intent smsintent=new Intent();
            smsintent.setAction(Intent.ACTION_VIEW);
            smsintent.setData(Uri.parse("sms:"));
            smsintent.putExtra("address","phonenumber");
            smsintent.putExtra("sms_body","message");
            startActivity(smsintent);
            return true;
        }
        return false;
    }
}

activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="me.rk.andses6ass4.MainActivity">

    <Button
        android:id="@+id/contextButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Context menu"
        android:layout_centerHorizontal="true"/>
</RelativeLayout>

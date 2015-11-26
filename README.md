# APK版本更新，软件下载更新，通知栏显示进度


    ![](http://i.imgur.com/aIf0s3r.gif)

首先你要添加权限

    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>


然后 只要启动一个服务就可以实现软件下载更新，通知栏显示进度

    package com.example.updateservice;
    
    import android.app.Activity;
    import android.app.AlertDialog;
    import android.app.AlertDialog.Builder;
    import android.app.Dialog;
    import android.content.Context;
    import android.content.DialogInterface;
    import android.content.Intent;
    import android.os.Bundle;
    
    public class MainActivity extends Activity {

	Context mContext;
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		mContext = this;
		showDialog();
	}
	
	private void showDialog(){
		AlertDialog.Builder builder = new Builder(mContext);
		builder.setTitle("升级提示");
		builder.setMessage("版本：1.0.1\n大小：6.5M\n1、修改Bug\n2、增加功能");
		builder.setNegativeButton("稍后再说", new AlertDialog.OnClickListener() {
			
			@Override
			public void onClick(DialogInterface dialog, int which) {
				dialog.dismiss();
				
			}
		});
		
		builder.setPositiveButton("马上跟新", new AlertDialog.OnClickListener() {
			
			@Override
			public void onClick(DialogInterface dialog, int which) {
				dialog.dismiss();
				Intent intent = new Intent(mContext,DownloadService.class);
				intent.putExtra("url", "http://surveyapp.fy.chaoxing.com/app/LauncherDemo5.apk");
				startService(intent);
			}
		});
		builder.show();
	}
    }


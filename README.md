import 'dart:async';
import 'package:flutter_bloc/flutter_bloc.dart';

abstract class AuthEvent {}

class LoginEvent extends AuthEvent {}

class LogoutEvent extends AuthEvent {}

abstract class AuthState {}

class LoggedOutState extends AuthState {}

class LoggedInState extends AuthState {}

class AuthBloc extends Bloc<AuthEvent, AuthState> {
  Timer? _logoutTimer;

  AuthBloc() : super(LoggedOutState()) {
    on<LoginEvent>((event, emit) {
      emit(LoggedInState());
      _startLogoutTimer();
    });

    on<LogoutEvent>((event, emit) {
      _logoutTimer?.cancel();
      emit(LoggedOutState());
    });
  }

  void _startLogoutTimer() {
    _logoutTimer?.cancel();
    _logoutTimer = Timer(Duration(minutes: 3), () {
      add(LogoutEvent());
    });
  }

  @override
  Future<void> close() {
    _logoutTimer?.cancel();
    return super.close();
  }
}
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

import 'auth_bloc.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocProvider(
      create: (_) => AuthBloc(),
      child: MaterialApp(
        home: AuthWrapper(),
      ),
    );
  }
}

class AuthWrapper extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocBuilder<AuthBloc, AuthState>(
      builder: (context, state) {
        if (state is LoggedOutState) {
          return LoginPage();
        } else if (state is LoggedInState) {
          return HomePage();
        } else {
          return SizedBox();
        }
      },
    );
  }
}

class LoginPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Login'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            context.read<AuthBloc>().add(LoginEvent());
          },
          child: Text('Login'),
        ),
      ),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            context.read<AuthBloc>().add(LogoutEvent());
          },
          child: Text('Logout'),
        ),
      ),
    );
  }
}


******---------******



<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.baseflow.permissionhandler.example">

    <uses-feature
        android:name="android.hardware.telephony"
        android:required="false" />
    <uses-feature
        android:name="android.hardware.camera"
        android:required="false" />

    <!--
    Internet permissions do not affect the `permission_handler` plugin, but are required if your app needs access to
    the internet.
    -->
    <uses-permission android:name="android.permission.INTERNET"/>

    <!-- Permissions options for the `contacts` group -->
    <uses-permission android:name="android.permission.READ_CONTACTS"/>
    <uses-permission android:name="android.permission.WRITE_CONTACTS"/>
    <uses-permission android:name="android.permission.GET_ACCOUNTS"/>

    <!-- Permissions options for the `storage` group -->
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <!-- Read storage permission for Android 12 and lower -->
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
    <!--
      Granular media permissions for Android 13 and newer.
      See https://developer.android.com/about/versions/13/behavior-changes-13#granular-media-permissions
      for more information.
    -->
    <uses-permission android:name="android.permission.READ_MEDIA_IMAGES" />
    <uses-permission android:name="android.permission.READ_MEDIA_VIDEO" />
    <uses-permission android:name="android.permission.READ_MEDIA_AUDIO" />

    <!-- Permissions options for the `camera` group -->
    <uses-permission android:name="android.permission.CAMERA"/>

    <!-- Permissions options for the `sms` group -->
    <uses-permission android:name="android.permission.SEND_SMS"/>
    <uses-permission android:name="android.permission.RECEIVE_SMS"/>
    <uses-permission android:name="android.permission.READ_SMS"/>
    <uses-permission android:name="android.permission.RECEIVE_WAP_PUSH"/>
    <uses-permission android:name="android.permission.RECEIVE_MMS"/>

    <!-- Permissions options for the `phone` group -->
    <uses-permission android:name="android.permission.READ_PHONE_STATE"/>
    <uses-permission android:name="android.permission.CALL_PHONE"/>
    <uses-permission android:name="android.permission.ADD_VOICEMAIL"/>
    <uses-permission android:name="android.permission.USE_SIP"/>
    <uses-permission android:name="android.permission.READ_CALL_LOG"/>
    <uses-permission android:name="android.permission.WRITE_CALL_LOG"/>
    <uses-permission android:name="android.permission.BIND_CALL_REDIRECTION_SERVICE"/>

    <!-- Permissions options for the `calendar` group -->
    <uses-permission android:name="android.permission.READ_CALENDAR" />
    <uses-permission android:name="android.permission.WRITE_CALENDAR" />

    <!-- Permissions options for the `location` group -->
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />

    <!-- Permissions options for the `microphone` or `speech` group -->
    <uses-permission android:name="android.permission.RECORD_AUDIO" />

    <!-- Permissions options for the `sensors` group -->
    <uses-permission android:name="android.permission.BODY_SENSORS" />
    <uses-permission android:name="android.permission.BODY_SENSORS_BACKGROUND" />

    <!-- Permissions options for the `accessMediaLocation` group -->
    <uses-permission android:name="android.permission.ACCESS_MEDIA_LOCATION" />

    <!-- Permissions options for the `activityRecognition` group -->
    <uses-permission android:name="android.permission.ACTIVITY_RECOGNITION" />

    <!-- Permissions options for the `ignoreBatteryOptimizations` group -->
    <uses-permission android:name="android.permission.REQUEST_IGNORE_BATTERY_OPTIMIZATIONS" />

    <!-- Permissions options for the `nearby devices` group -->
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.BLUETOOTH_SCAN" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADVERTISE" />
    <uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
    <uses-permission android:name="android.permission.NEARBY_WIFI_DEVICES" />

    <!-- Permissions options for the `manage external storage` group -->
    <uses-permission android:name="android.permission.MANAGE_EXTERNAL_STORAGE" />

    <!-- Permissions options for the `system alert windows` group -->
    <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />

    <!-- Permissions options for the `request install packages` group -->
    <uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES" />

    <!-- Permissions options for the `access notification policy` group -->
    <uses-permission android:name="android.permission.ACCESS_NOTIFICATION_POLICY"/>

    <!-- Permissions options for the `notification` group -->
    <uses-permission android:name="android.permission.POST_NOTIFICATIONS"/>

    <!-- Permissions options for the `alarm` group -->
    <uses-permission android:name="android.permission.SCHEDULE_EXACT_ALARM" />

    <application
        android:name="${applicationName}"
        android:icon="@mipmap/ic_launcher"
        android:label="permission_handler_example"
        tools:ignore="AllowBackup,GoogleAppIndexingWarning">

        <activity android:name="io.flutter.embedding.android.FlutterActivity"
            android:launchMode="singleTop"
            android:theme="@android:style/Theme.Black.NoTitleBar"
            android:configChanges="orientation|keyboardHidden|keyboard|screenSize|locale|layoutDirection"
            android:hardwareAccelerated="true"
            android:windowSoftInputMode="adjustResize"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>

        <meta-data
            android:name="flutterEmbedding"
            android:value="2" />
    </application>
</manifest>




# linux cheatsheet
## Linux Basic Command
<br/>1.ls		 {Lists all files and directories in the present working directory}
<br/>2.ls -R 	{Lists files in sub-directories as well}
<br/>3.ls -a		{Lists hidden files as well}
<br/>4.ls -al		{Lists files and directories with detailed information like permissions,size, owner, etc.}
<br/>5.cd or cd 	{	Navigate to HOME directory}
<br/>6.cd ..			{Move one level up}
<br/>7.cd	 	{To change to a particular directory}
<br/> cd /folder/folder/folder {direct path}
<br/>8.cd /	 	{Move to the root directory}
<br/>9.cat > filename		{ Creates a new file}
<br/>10.cat filename		{Displays the file content}
<br/>11.cat file1 file2 > file3		{Joins two files (file1, file2) and stores the output in a new file (file3)}
<br/>12.mv file "new file path"		{Moves the files to the new location}
<br/>13.mv filename new_file_name		{Renames the file to a new filename}
<br/>14.pwd 	{Show current directory}
<br/>15.rm filename		{Deletes a file}
<br/>16.history		{Gives a list of all past commands typed in the current terminal session}
<br/>17.clear		{Clears the terminal}
<br/>18.rmdir		{Deletes a directory}
<br/>19.mv		{Renames a directory}
<br/>20.pr -x		{Divides the file into x columns}
<br/>21.pr -h		{Assigns a header to the file}
<br/>22.apt-get 	{Command used to install and update packages}
<br/>
## File Permission
<br/>1.ls -l		{to show file type and access permission}
<br/>2. r		{read permission}
<br/>3.w 		{write permission}
<br/>4.x 		{execute permission}
<br/>5. Chown user		{For changing the ownership of a file/directory}
<br/>6. chmod u+x file_name {add execute permissions for the owner}
<br/>7. chmod g+rw file_name{dd read and write permissions for the group }
# Apache for static web
### uninstall Apache2
<br/>sudo service apache2 stop
<br/>sudo apt-get remove apache2
<br/>sudo apt-get purge apache2
<br/>sudo apt-get autoremove
<br/>sudo rm -rf /etc/apache2
## install apache2
</br>apt-get install httpd -y
<br/>sudo apt-get install apache2
<br/>apache2 -version
### SSH Connection
<br/>ssh -i nibir.pem username(ubuntu)@3.86.200.159
<br/>sudo su
<br/>sudo apt-get update
<br/>systemctl status apache2
<br/>cd var/www/html/
<br/> use nano for edit index.html
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>



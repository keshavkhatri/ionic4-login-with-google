create dummy project with 
ionic start
enter the project name
pick starter template 
sidemenu in this case
no to ionic appflow
go to directory
run ionic serve
create a button login with google on homepage
using ion-button
now go to https://console.firebase.google.com
login with your google account
create new project there
remove google analytics for the project
click on android icon to add to your project 
it will ask few things like android package name, app nick name, sha1 id
package name you can find it in the cofing xml and should change it (if not found config.xml then run "ionic cordova platform add android")
app nick name is option and your choice
sha1 id can be generated using
keytool -exportcert -list -v -alias androiddebugkey -keystore ~/.android/debug.keystore
if asked for password use "android"
download google-services.json
leave the rest by clicking next
now register app for ios as well
it will ask for few details like ios bundle id, nickname, app store id.
bundle id is the same which we picked from config xml
rest is optional leave it
download the config file GoogleService-Info.plist and put it in root folder
click next and leave rest
open the file and copy REVERSED_CLIENT_ID
install plugni using below command
com.googleusercontent.apps.1022784222942-ohmn1e09c15notmn7inocqpjf0n2ludd
cordova plugin add cordova-plugin-googleplus --save --variable REVERSED_CLIENT_ID=myreversedclientid
replace myreversedclientid with your id found in GoogleService-Info.plist
then install npm package using 
npm install --save @ionic-native/google-plus
run below command
cordova prepare
now go to authentication section in you project in firebase console
go to sign in methods section
enable login with google (it would be disabled by default)
click on save after editing the current settings
add "import { GooglePlus } from '@ionic-native/google-plus/ngx';" in the app.module.ts
add it to providers array
now do the same in home.page.ts
import { GooglePlus } from '@ionic-native/google-plus/ngx';
constructor(private googlePlus: GooglePlus) {}
loginWithGoogle() {
        this.googlePlus.login({
        })
        .then(res => console.log(res))
        .catch(err => console.error(err));
    }


======================================

12500 google login error
due to google sign in not enabled

10 google login error
due to sha1 or package name mismatch

success response
accessToken: "ya29.Il-2BzU5Q4ztC0U0ngFVAXxWWfJtx2YQCUufySfi3rJpJBHDbq0cYnOf9rXmUDwmJVfpFzTmR5OGZuYAz7jOqjfbHPh_4XN3luA0yv6EMVEZSLRuVZ_y604Vy8MXWaemJA"
displayName: "Keshav Khatri"
email: "keshav8khatri@gmail.com"
expires: 1577110170
expires_in: 3599
familyName: "Khatri"
givenName: "Keshav"
userId: "100104156798821092888"

=======================================

you can request user data in google

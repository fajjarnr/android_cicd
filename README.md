
### generate keystore
`keytool -genkeypair -v -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000`

move keystore to **/app**

add to **gradle.properties**

    MYAPP_UPLOAD_STORE_FILE=my-upload-key.keystore
    MYAPP_UPLOAD_KEY_ALIAS=my-key-alias
    MYAPP_UPLOAD_STORE_PASSWORD=<password>
    MYAPP_UPLOAD_KEY_PASSWORD=<password>

add to **/app/build.gradle**

    signingConfigs{
        release {
            if (project.hasProperty('MYAPP_UPLOAD_STORE_FILE')){
                storeFile file(MYAPP_UPLOAD_STORE_FILE)
                storePassword MYAPP_UPLOAD_STORE_PASSWORD
                keyAlias MYAPP_UPLOAD_KEY_ALIAS
                keyPassword MYAPP_UPLOAD_KEY_PASSWORD
            }
        }
    }

add to **buildType{}**

    signingConfig signingConfigs.release

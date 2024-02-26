# android-sdk-public

## Install

Register on Github and create a personal access token with `read:packages` permission. Add your Github username and token as an environmental variables.
Add the following to the Android project `build.gradle` project:

```
allprojects {
        repositories {
            maven {
                name = "GitHub"
                url = uri("https://maven.pkg.github.com/getivy/android-sdk-public")
                credentials {
                    username = System.getenv("GITHUB_USER")
                    password = System.getenv("GITHUB_TOKEN")
                }
            }
        }
    }
```

Add the following to the `app/build.gradle` file:

```
implementation 'io.getivy:sdk:2.+'
```

## Usage

Initialize the SDK with a checkout or data session:

```
import io.getivy.sdk.GetivySDK
import io.getivy.sdk.data.SDKFlowType
import io.getivy.sdk.handler.Handler

// OTHER CODE

GetivySDK.createHandler(
    context = <application/activity context>,
    sessionId = <checkout/data session id>,
    type = <SDKFlowType.DATA or SDKFlowType.CHECKOUT,
    environment = "production" or "sandbox")
{ handler ->
    // Retain the handler
    this.handler = handler
}
```

Opening the SDK UI:

```
this.handler.open {
    when (it) {
        is Handler.Result.Success -> {
          // SDK flow ended with success e.g. user paid successfuly
        }
        is Handler.Result.Error -> {
          // SDK flow finished with an error e.g. user closed the UI manually
        }
      }
}
```




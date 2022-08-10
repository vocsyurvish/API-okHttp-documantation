# API-okHttp-documantation

#### Import library in your project...

```grovy
    //okhttp
    implementation(platform("com.squareup.okhttp3:okhttp-bom:4.9.0"))
    implementation("com.squareup.okhttp3:okhttp")
    implementation("com.squareup.okhttp3:logging-interceptor")
    // gson
    implementation 'com.google.code.gson:gson:2.9.0'
```

#### in Manifest.xml

```xml

android:usesCleartextTraffic="true"

```

#### Create java class into your project as a `JsonUtils`

<Details>
<Summary> click to open class </Summary>

#### JsonUtils.java

```java

public class JsonUtils {

    public static String okhttpGET(String url) {
        OkHttpClient client = new OkHttpClient.Builder()
                .readTimeout(20000, TimeUnit.MILLISECONDS)
                .writeTimeout(20000, TimeUnit.MILLISECONDS)
                .build();

        Request request = new Request.Builder()
                .url(url)
                .build();

        try {
            Response response = client.newCall(request).execute();
            return response.body().string();
        } catch (Exception e) {
            e.printStackTrace();
            return "";
        }
    }

    public static String okhttpPost(String url, RequestBody requestBody) {
        OkHttpClient client = new OkHttpClient.Builder()
                .readTimeout(25000, TimeUnit.MILLISECONDS)
                .writeTimeout(25000, TimeUnit.MILLISECONDS)
                .build();

        Request request = new Request.Builder()
                .url(url)
                .post(requestBody)
                .build();

        try {
            Response response = client.newCall(request).execute();
            return response.body().string();
        } catch (Exception e) {
            e.printStackTrace();
            return "";
        }
    }
}

```

</Details>

#### Get Response into String...

```java
// get
String json = JsonUtils.okhttpGet("url");
// post
String json = JsonUtils.okhttpPost("url", REQUEST_BODY);
```

#### How to impliment RequestBody

<Details>
<Summary> click to view RequestBody </Summary>

#### Normal

```java

public RequestBody getAPIRequest(){
  JsonObject jsObj = (JsonObject) new Gson().toJsonTree(new API());
  jsObj.addProperty("KEY", PARAMS);
  jsObj.addProperty("KEY", PARAMS);
  //...
  
  return new MultipartBody.Builder()
         .setType(MultipartBody.FORM)
         .addFormDataPart("data", jsObj.toString())
         .build();
}

```
#### with image

```java

public RequestBody getAPIRequest(File file){
  JsonObject jsObj = (JsonObject) new Gson().toJsonTree(new API());
  jsObj.addProperty("KEY", PARAMS);
  jsObj.addProperty("KEY", PARAMS);
  //...
  
  return new MultipartBody.Builder()
         .setType(MultipartBody.FORM)
         .addFormDataPart("user_image", file.getName(), RequestBody.create(MediaType.parse("image/*"), file))
         .addFormDataPart("data", jsObj.toString())
         .build();
}

```


</Details>

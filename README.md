# retrofit2-jsonobject-converter
A Retrofit 2 converter to convert your request and response data to org.json.JSONObject.

# Compatibility

Tested with Retrofit 2.0.0-beta2

# Usage

Register the converter:

```java
OkHttpClient client = new OkHttpClient();
Retrofit restAdapter = new Retrofit.Builder()
        .baseUrl(endPoint)
        .client(client)
        .addConverterFactory(JsonConverterFactory.create())
        .build();

api = restAdapter.create(PdApiInterface.class);
```

In your API interface file:

```java
@POST("/v2/package")
    Call<JSONObject> subscribePackage(@Body JSONObject data);

@GET("/v2/account/{id}")
    Call<JSONObject> getAccount(@Path("id") int id);
```

Then in your code:

```java
Call c = api.getAccount(getApiManager().getAccountId());
c.enqueue(new Callback<JSONObject>() {
    @Override
    public void onResponse(Response<JSONObject> response, Retrofit retrofit) {
        if (response.isSuccess()) {
            // response.body() is a JSONObject
            onDataReceived(response.body());
        }
    }

    @Override
    public void onFailure(Throwable t) {

    }
});

```
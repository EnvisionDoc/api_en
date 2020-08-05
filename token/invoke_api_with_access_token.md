# Invoking API with Access Token

<br />

Follow the instructions below to invoke EnOS APIs with the generated access token.

## Before You Start

- Before invoking an EnOS API with the access token, you need to have the values of **appKey**, **appSecret**, **accessToken**, and **timestamp** ready.


## Procedure

### Constructing `paramsData`

1. Sort all the parameters of the API in the URL by ASCII order.

2. Concatenate the sorted parameters and their values into a string.

3. If the API request requires a JSON formatted request body, append the request body after the concatenated string to form the `paramsData`.

.. note:: The request body that is included in the `paramsData` must be identical with what is set in the API request. Otherwise, the verification will fail.


### Constructing `apim-sign`

1. Concatenate the values of `accessToken`, `paramsData`, `timestamp`, and `appSecret` into a string to form the `signData`.

2. Encode the concatenated string `signData` in UTF-8 format and make a digest by **SHA256** algorithm.

3. Convert the digest to hexadecimal format to generate the encrypted ciphertext `apim-sign`. See the following pseudo code:

```
sha256(signData).toLowerCase();
```

### Constructing the Request Header

Include the following parameters in the API request header:

```
apim-accesstoken: accessToken
apim-signature: apim-sign
apim-timestamp: timestamp
```

## Error Codes

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Description
   * - 0
     - Success
   * - 1001
     - Repeated requests with duplicated ``encryption``.
   * - 1002
     - The ``appKey`` does not exist.
   * - 1003
     - The ``encryption`` is not valid.
   * - 1004
     - Invalid parameter.
   * - 1005
     - Internal service exception.
   * - 1202
     - The parameter is empty.
   * - 1203
     - The access token has expired.
   * - 1204
     - Failed to refresh access token.


## Sample

The following example shows the steps of invoking an API with the access token.

### Request URL
```
https://{apigw-address}/m/v1/b?k3=v3&k1=v1&k2=v2
```

### Request Body

```json
{
  "count": 20,
  "page": 1,
  "desc": "description"
}
```

### Request Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Parameter
     - Value
   * - accessToken
     - xxxxaaaxxxx
   * - appSecret
     - xxxappSecretxxx
   * - timestamp
     - 1572574909697

### Request Steps

Take the following steps to invoke the API with access token:

1. Sort the parameters k3, k1, k2 in the URL by ASCII order into k1, k2, k3.

2. Concatenate the sorted parameters and their values into a string, for example, `k1v1k2v2k3v3`.

3. Concatenate the string `k1v1k2v2k3v3` and the request body into the following:

  ```
  k1v1k2v2k3v3{
  "count": 20,
  "page": 1,
  "desc": "description"
  }
  ```

4. Concatenate the values of `accessToken`, `paramsData`, `timestamp`, and `appSecret` into the following:

  ```
  xxxxaaaxxxxk1v1k2v2k3v3{
  "count": 20,
  "page": 1,
  "desc": "description"
  }1572574909697xxxappSecretxxx
  ```

5. Encode the above concatenated string in UTF-8 format and make a digest by **SHA256** algorithm. Convert the digest to hexadecimal format to generate a signature like the following example:

   ```
   59828328f6c1f9771015dc74e4929ae30f518a35a3d2353972c2ea46556fc981
   ```

6. Send the API request, for example:

   ```
   curl https://{apigw-address}/m/v1/b?k3=v3&k1=v1&k2=v2 -X POST
   -H 'apim-accesstoken:xxxxaaaxxxx'
   -H 'apim-signature:59828328f6c1f9771015dc74e4929ae30f518a35a3d2353972c2ea46556fc981'
   -H 'apim-timestamp:1572574909697'
   -d '{
   "count": 20,
   "page": 1,
   "desc": "description"
   }'
   ```

### Java Request Sample

```java
import okhttp3.*;

import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
import java.util.Collections;
import java.util.List;
import java.util.stream.Collectors;

/**
 * @author lixiangxin
 * @date 2019/10/24 18:56
 **/
public class EncryptUtils {

    /**
     * Encryption with Java Class
     *
     * @param str Encrypted string
     * @return
     */
    public static String getSHA256(String str) {
        MessageDigest messageDigest;
        String encodestr = "";
        try {
            messageDigest = MessageDigest.getInstance("SHA-256");
            messageDigest.update(str.getBytes(StandardCharsets.UTF_8));
            encodestr = hexString(messageDigest.digest());
        } catch (NoSuchAlgorithmException e) {
            return encodestr;
        }

        return encodestr;
    }

    private static String hexString(byte[] b) {
        StringBuilder hs = new StringBuilder();
        String stmp;
        for (int n = 0; b != null && n < b.length; n++) {
            stmp = Integer.toHexString(b[n] & 0XFF);
            if (stmp.length() == 1) {
                hs.append('0');
            }
            hs.append(stmp);
        }
        return hs.toString();
    }

    public static void main(String[] args) throws IOException {

        String accssToken = "xxxxaaaxxxx";
        String appSecret = "xxxappSecretxxx";
        long timestamp = 1572574909697L; //System.currentTimeMillis();

        String url = "https://{apigw-address}/m/v1/b?k3=v3&k1=v1&k2=v2";
        String requestBody = "{\n" +
                "  \"count\": 20,\n" +
                "  \"page\": 1,\n" +
                "  \"desc\": \"description\"\n" +
                "}";

		HttpUrl httpUrl = HttpUrl.parse(url);
        if (httpUrl == null) {
            return;
        }

        List<String> keys = new ArrayList<>(httpUrl.queryParameterNames());
        Collections.sort(keys);

        StringBuilder paramsData = new StringBuilder();
        for (String key : keys) {
            String value = httpUrl.queryParameter(key);
            paramsData.append(key).append(value);
        }
        paramsData.append(requestBody);
        String signData = accssToken + paramsData.toString() + timestamp + appSecret;
        String apimSign = getSHA256(signData);

        RequestBody body = FormBody
                .create(MediaType.parse("application/json; charset=utf-8"), requestBody);

        Request request = new Request.Builder().url(url).method("POST", body)
                .addHeader("apim-accesstoken", accssToken)
                .addHeader("apim-signature", apimSign)
                .addHeader("apim-timestamp", timestamp + "")
                .build();

        String res = new OkHttpClient().newCall(request).execute().body().string();
        System.out.println(res);
    }
}
```

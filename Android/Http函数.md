# Http函数

```java
public class Http {

    private static final int TIMEOUT = 10000;			//设置连接超时

    /**
     * Http Get
     * @param host  地址
     * @return  Http响应
     */
    public static String get(String host) {
        int httpCode = HttpConstant.RESP_FAILED;
        String httpResp;
        HttpURLConnection connection = null;
        try {
            URL url = new URL(host);
            connection = (HttpURLConnection) url.openConnection();
            connection.setConnectTimeout(TIMEOUT);
            connection.setReadTimeout(TIMEOUT);
            int responseCode = connection.getResponseCode();
            if (responseCode == HttpsURLConnection.HTTP_OK) {
                InputStream in = new BufferedInputStream(connection.getInputStream());
                BufferedReader reader = new BufferedReader(new InputStreamReader(in));
                String line;
                StringBuffer sb = new StringBuffer();
                while ((line = reader.readLine()) != null) {
                    sb = sb.append(line).append("\n");
                }
                String response = sb.toString();
                LogUtil.i("http get response=" + response);
                return response;
            } else {
                httpCode = responseCode;
                httpResp = connection.getResponseMessage();
            }
        } catch (Exception e) {
            e.printStackTrace();
            httpResp = e.getMessage();
        } finally {
            if (connection != null) {
                connection.disconnect();
            }
        }
        JSONObject jsonObject = new JSONObject();
        try {
            jsonObject.put("status", httpCode);
            jsonObject.put("info", httpResp);
        } catch (JSONException e) {
            e.printStackTrace();
        }
        return jsonObject.toString();
    }

    /**
     * 下载文件
     * @param fileUrl   文件地址
     * @return          字节
     */
    public static byte[] download(String fileUrl) {
        HttpURLConnection connection = null;
        try {
            URL url = new URL(fileUrl);
            connection = (HttpURLConnection) url.openConnection();
            connection.setConnectTimeout(TIMEOUT);
            connection.setReadTimeout(TIMEOUT);
            int responseCode = connection.getResponseCode();
            if (responseCode == HttpsURLConnection.HTTP_OK) {
                InputStream in = new BufferedInputStream(connection.getInputStream());
                ByteArrayOutputStream outStream = new ByteArrayOutputStream();
                byte[] buffer = new byte[1024];
                int len;
                while((len=in.read(buffer)) != -1){
                    outStream.write(buffer, 0, len);
                }
                outStream.close();
                in.close();
                byte[] b = outStream.toByteArray();
                LogUtil.i("http download file success! url=" + fileUrl);
                return b;
            } else {
                return null;
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            if (connection != null) {
                connection.disconnect();
            }
        }
        return null;
    }

    /**
     * Http Post
     * @param url           地址
     * @param body          请求数据
     */
    public static String postUrlencoded(String url, String body) {
        LogUtil.i("http post url=" + url);
        int httpCode = HttpConstant.RESP_FAILED;
        String httpResp;
        HttpURLConnection connection = null;
        try {
            URL mUrl = new URL(url);
            connection = (HttpURLConnection) mUrl.openConnection();
            connection.setRequestMethod("POST");//设置方法
            connection.setDoOutput(true);//设置可输出
            connection.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");//如果是JSON则填application/json
            connection.setChunkedStreamingMode(0);
            connection.setConnectTimeout(TIMEOUT);
            connection.setReadTimeout(TIMEOUT);
            OutputStream out = connection.getOutputStream();
            BufferedWriter writer = new BufferedWriter(
                    new OutputStreamWriter(out, "UTF-8"));//封装输出流
            writer.write(body);
            writer.flush();
            writer.close();
            out.close();
            //获得响应
            int responseCode = connection.getResponseCode();
            if (responseCode == HttpURLConnection.HTTP_OK) {
                InputStream in = new BufferedInputStream(connection.getInputStream());
                BufferedReader reader = new BufferedReader(new InputStreamReader(in));
                String line;
                StringBuffer sb = new StringBuffer();
                while ((line = reader.readLine()) != null) {
                    sb = sb.append(line).append("\n");
                }
                String response = sb.toString();
                LogUtil.i("http post response = " + response);
                return response;
            } else {
                httpCode = responseCode;
                httpResp = connection.getResponseMessage();
            }
        } catch (Exception e) {
            e.printStackTrace();
            httpResp = e.getMessage();
        } finally {
            if (connection != null) {
                connection.disconnect();
            }
        }
        JSONObject jsonObject = new JSONObject();
        try {
            jsonObject.put("status", httpCode);
            jsonObject.put("info", httpResp);
        } catch (JSONException e) {
            e.printStackTrace();
        }
        return jsonObject.toString();
    }

    /**
     * 拼接url地址或者参数
     * @param urlPath   地址，如果Post方法则填""，只拼接参数
     * @param params    参数
     * @return          发起请求的参数
     */
    public static String buildUrlOrParams(String urlPath, Map<String, Object> params) {
        if (urlPath == null || params == null || params.size() == 0) {
            return "";
        }
        StringBuilder sb = new StringBuilder();
        Set<String> keys = params.keySet();
        for (String key : keys) {
            if (params.get(key) == null) {
                continue;
            }
            sb = sb.append(key).append("=").append(URLEncoder.encode(params.get(key).toString())).append("&");
        }
        String urlParams = sb.substring(0, sb.length() - 1);
        if (urlPath.length() == 0) {
            LogUtil.i("buildUrlOrParams = " + urlParams);
            return urlParams;
        } else {
            if (!urlPath.endsWith("?")) {
                urlPath += "?";
            }
            String urlString = urlPath + urlParams;
            LogUtil.i("buildUrlOrParams = " + urlString);
            return urlString;
        }
    }

   
}

```
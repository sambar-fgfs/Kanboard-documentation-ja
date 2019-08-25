API の例
============

cURLを使用する例
-----------------

特別なユーザー ``jsonrpc`` を使用する例:

.. code:: bash

    curl \
    -u "jsonrpc:19ffd9709d03ce50675c3a43d1c49c1ac207f4bc45f06c5b2701fbdf8929" \
    -d '{"jsonrpc": "2.0", "method": "getAllProjects", "id": 1}' \
    http://localhost/kanboard/jsonrpc.php

通常のユーザーでは:

.. code:: bash

    curl \
    -u "*ユーザー名*:*シークレット* \
    -d '{"jsonrpc": "2.0", "method": "getMyProjects", "id": 1}' \
    http://localhost/kanboard/jsonrpc.php


サーバーからのレスポンス:

.. code:: json

    {
        "jsonrpc":"2.0",
        "id":1,
        "result":[
            {
                "id":"1",
                "name":"API test",
                "is_active":"1",
                "token":"6bd0932fe7f4b5e6e4bc3c72800bfdef36a2c5de2f38f756dfb5bd632ebf",
                "last_modified":"1403392631"
            }
        ]
    }

Pythonを使用する例
-------------------

これが `Kanboardの公式Pythonクライアント <https://github.com/kanboard/kanboard-api-client>`__ です:

.. code:: bash

    pip install kanboard

これはプロジェクトとタスクを作成する例です:

.. code:: python

    import kanboard

    kb = kanboard.Client('http://localhost/jsonrpc.php', 'jsonrpc', 'your_api_token')

    project_id = kb.create_project(name='My project')
    kb.add_project_user(project_id=project_id, user_id=123, role='project-manager')

    task_id = kb.create_task(project_id=project_id, title='My task title')

Rubyを使用する例
-----------------

この例は、APIでカスタム認証ヘッダを使用するように設定し、リバースプロキシも利用するように設定されたKanboardで利用可能です:

.. code:: ruby

    require 'faraday'

    conn = Faraday.new(:url => 'https://kanboard.example.com') do |faraday|
        faraday.response :logger
        faraday.headers['X-API-Auth'] = 'XXX'      # base64_encode('jsonrpc:API_KEY')
        faraday.basic_auth(ENV['user'], ENV['pw']) # user/pass to get through basic auth
        faraday.adapter Faraday.default_adapter    # make requests with Net::HTTP
    end

    response = conn.post do |req|
        req.url '/jsonrpc.php'
        req.headers['Content-Type'] = 'application/json'
        req.body = '{ "jsonrpc": "2.0", "id": 1, "method": "getAllProjects" }'
    end

    puts response.body

Javaを使用する例
-----------------

Spring を使用する基本的な例です。正確な使用方法は `このリンク <http://spring.io/guides/gs/consuming-rest>`__ を参照願います。

.. code:: java

    import java.io.UnsupportedEncodingException;
    import java.util.Base64;

    import org.springframework.http.HttpEntity;
    import org.springframework.http.HttpHeaders;
    import org.springframework.http.MediaType;
    import org.springframework.web.client.RestTemplate;

    public class ProjectService {

        public void getAllProjects() throws UnsupportedEncodingException {

            RestTemplate restTemplate = new RestTemplate();

            String url = "http://localhost/kanboard/jsonrpc.php";
            String requestJson = "{\"jsonrpc\": \"2.0\", \"method\": \"getAllProjects\", \"id\": 1}";
            String user = "jsonrpc";
            String apiToken = "19ffd9709d03ce50675c3a43d1c49c1ac207f4bc45f06c5b2701fbdf8929";

            // encode api token
            byte[] xApiAuthTokenBytes = String.join(":", user, apiToken).getBytes("utf-8");
            String xApiAuthToken = Base64.getEncoder().encodeToString(xApiAuthTokenBytes);

            // consume request
            HttpHeaders headers = new HttpHeaders();
            headers.add("X-API-Auth", xApiAuthToken);
            headers.setContentType(MediaType.APPLICATION_JSON);
            HttpEntity<String> entity = new HttpEntity<String>(requestJson, headers);
            String answer = restTemplate.postForObject(url, entity, String.class);
            System.out.println(answer);
        }
    }

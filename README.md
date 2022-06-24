# sam-lambda-urls1

[AWS Lambda Function URLs](https://aws.amazon.com/jp/blogs/aws/announcing-aws-lambda-function-urls-built-in-https-endpoints-for-single-function-microservices/)
の最初のサンプル。

とりあえず認証なし、CORSなしで。Lambda本体はpython 3.8


# デプロイ

```sh
sam build
sam deploy --guided  # --guidedは最初の1回だけ
```

設定値はデフォルトでいいです。


# テスト

stackのoutputの `HelloWorldFunctionUrl` をcurlで呼んでください。

実行例:
```
$ curl https://xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.lambda-url.ap-northeast-1.on.aws/
{"body": "hello world\n"}
```


# スタックの削除

```sh
sam delete --no-prompts
```
で消えます。
いま認証なしなんで、動作確認したらさっさと消したほうがいいと思います。


# メモ

まだ AWS::Lambda::Url リソースのドキュメントがないけど、
URLのアトリビュートは .FunctionUrl でした。

## 追記(2022-04-11)

ドキュメント出た。
[AWS::Lambda::Url - AWS CloudFormation](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-url.html)

AuthTypeについては
[Security and auth model for Lambda function URLs - AWS Lambda](https://docs.aws.amazon.com/ja_jp/lambda/latest/dg/urls-auth.html)

# IAM認証追加してみた

AWS_IAMブランチで。

[awscli](https://github.com/okigan/awscurl)で、
```bash
awscurl --service lambda --region ap-northeast-1 "$TheURL"
```

みたいにしてください。

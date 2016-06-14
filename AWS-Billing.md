cli
----

[【Hubot】AWSの利用料金を聞くと答えてくれるようにした - Qiita](http://qiita.com/kingpanda/items/aa1b24ffd12dd81f1ab2)

```bash
$ aws cloudwatch --region us-east-1 get-metric-statistics \
>     --namespace "AWS/Billing" \
>     --metric-name "EstimatedCharges" \
>     --dimensions "[{\"Value\":\"AmazonEC2\",\"Name\":\"ServiceName\"},{\"Value\":\"USD\",\"Name\":\"Currency\"}]" \
>     --period 60 \
>     --start-time `date -u -d '3 hours ago' +%Y-%m-%dT%TZ` \
>     --end-time `date -u +%Y-%m-%dT%TZ` \
>     --statistics "Maximum" \
>      | jq '.Datapoints | sort_by(.Timestamp) | reverse | .[0]'
```
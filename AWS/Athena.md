## Athena
`Amazon Athena`は、SQLによって`Amazon S3`に保存されたデータを容易に抽出できるサービス。  
利用する際はAWSのコンソールからデータが保存されている場所を指定し、クエリを実行する。

例えばWebサービスのアクセスログをS3に保存していたら、調査が必要な時はAthenaによって
条件指定でログを素早く検索できる。

CSVやJSONなどの形式や、Apache Parquetなどの列志向のデータにも対応している。
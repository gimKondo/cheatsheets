# GCPチートシート
## SDK
### フィルタの使い方
- https://cloud.google.com/sdk/gcloud/reference/topic/filters

### gloud compute
- インスタンス一覧
    - 全部: `gcloud compute instances list`
    - 名前でフィルタ: `gcloud compute instances list --filter="name('NAME1' 'NAME2')"`

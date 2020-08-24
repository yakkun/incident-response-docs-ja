---
cover: assets/img/covers/alerting_principles.png
description: We manage how we get alerted based on a simple principle, an alert is something which requires a human to perform an action. Anything else is a notification, which is something that we cannot control, and for which we cannot make any action to affect it. Notifications are useful, but they shouldn't be waking people up under any circumstance.
---

私たちは、**アラートは人手によるアクションが必要** というシンプルな原則に基づいて、アラートを管理します。
それ以外の我々で制禦できないものは通知であり、それに対するアクションもできません。
通知は便利ですが、いかなる状況でも人々を目覚めさせてはいけません。


## アラートの優先度

!!! warning "再優先度アラート"

    深夜に人を叩き起こすものは **すぐに人が対応できるもの** であるべきです。
    そうでなければ、人々を呼び出さないようアラートを調整する必要があります。

| 優先度       | アラート                           | 対応                             |
| --------     | ------                             | --------                         |
| High         | 高優先度アラート（24/365）         | 人手による**緊急対応**が必要     |
| Medium       | 高優先度アラート（**業務時間内**） | 24時間以内に人手による対応が必要 |
| Low          | 低優先度アラート（24/365）         | いずれか人手による対応が必要     |
| Notification | 抑制されたイベント                 | 対応不要、情報のみ               |

新しいアラート/通知を設定する場合は、誰に通知したいかを考えてください。
たとえば、即時対応が必要ない場合は、高優先アラートを鳴らさないよう注意してください。

## 優先度の例

#### 本番サービスで75%のリクエストが失敗して、自動で解決しない

優先度**High**で、すぐに人手による対応が必要です。

![High Urgency](../assets/img/screenshots/high_urgency.png)

#### 本番サーバーのディスクが枯渇して、48時間以内にディスクフルになる。ログローテーションでは解決しない。

優先度**Medium**で、すぐにではないが人手による対応が必要になります。。

![Medium Urgency](../assets/img/screenshots/high_business_hours.png)

#### 1週間以内にSSL証明書が失効する

これは優先度**Low**で、人手による対応がそのうち必要です。

![Low Urgency](../assets/img/screenshots/low_urgency.png)

#### デプロイが成功した

これは**Notification**で、イベントは抑制されて送信されるべきです。
これはインシデント発生時に役立つ情報ですが、人間に知らせる必要はありません。

![Notification](../assets/img/screenshots/suppressed.png)

## アラートの内容

アラートには問題を迅速に特定できる文脈と、復旧できる可能性がある手順を含むべきです。
アラートに一般的なタイトルまたは説明文を使うと返って混乱を招く可能性があります。
私たちにはアラートの内容に関する一連のガイドアリンがあり、全てのアラートがそれに従うべきです。

#### タイトルやサマリーは説明的で簡潔にする
  * <span class="bad">&#x2718;</span> ALERT: 何かが壊れた
  * <span class="good">&#x2713;</span> `prod-web-loadbalancer-af5462ce` でディスク使用量が80%になった

#### 本文のどこかに、トリガーされたメトリクスを載せる
  * <span class="bad">&#x2718;</span> ディスク空き容量が枯渇しています
  * <span class="good">&#x2713;</span> `avg(last_1h):max:system.disk.in_use{env:prod-web-loadbalancer} by {host} > 0.8`

#### 本文には実際に何が問題で、なぜ問題なのかを載せる
  * <span class="bad">&#x2718;</span> ディスクがいっぱいです
  * <span class="good">&#x2713;</span> ディスクの使用量が80%になりました。もしディスクがいっぱいになると、ファイルを作成したり卯川期ができなくなり、システムが不安定になります。

#### 問題を解決する明確な手順や手順書へのリンクを載せる。
  * <span class="bad">&#x2718;</span> 削除して直してください
  * <span class="good">&#x2713;</span> 手順書 (https://example.com/runbook/disk) を参考にして、ディスクの空き容量を確保してください。再発防止のために、手順書 (https://example.com/runbook/log-rotate) に従って、ログローテーションのしきい値の設定が十分か調査してください。

## アラートをテストする


!!! info "テストは重要です"
    テストしていなアラートは、アラートが無いのと同じです。
    いざという時、アラートが動作するかわかりません。
    アラートが実際に動作するかをテストするのは、正常なサービス運用にとって重要で、リリースの計画やデプロイのデプロイ作業に含めるべきです。

追加されたアラートは必ずテストしてください。
これは新しいサービスの[金曜日の障害](https://www.pagerduty.com/blog/failure-friday-at-pagerduty/)によってカバーされますが、より迅速にする場合は手動でテストしてください。
テストすべきものは

* 閾値が適切に設定されているか。ノイズの多いアラートは必要ないです。
* データが無い状態 (No Data) でアラートが鳴るかどうか。通常データが無いというのは、閾値を超えることと同じです。
* メトリクスが通常状態に戻ったとき、アラートは自動で解決するかどうか。
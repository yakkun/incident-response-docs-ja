---
cover: assets/img/covers/post-mortem_template.png
description: これはPagerDutyで利用している標準的なポストモーテムのテンプレートです。それぞれのセクションでは、あなたがポストモーテムに書くべき情報について説明します。
---

これはPagerDutyで利用している標準的なポストモーテムのテンプレートです。
それぞれのセクションでは、あなたがポストモーテムに書くべき情報について説明します。

---

!!! note "ガイドライン"
    このページはインシデント発生後5営業日以内に設定されるポストモーテムのミーティングで確認することを目的とします。
    最初のステップはインシデント発生の5営業日以内に、共有カレンダーにミーティングを設定することです。
    情報が埋まるまでミーティングの設定を待ってはいけませんが、ミーティングまでにページができているようにしてください。

** ポストモーテムのオーナー:** _ここにはあなたの名前が入ります。_

** ミーティングの対象:** _インシデント発生後5営業日以内に、「インシデントポストモーテムミーティング」を共有カレンダーにスケジュールします。ここに日付を入力してください_

** 通話の記録:** _インシデントの通話の記録へのリンクを貼る。_

## オーバービュー

_**短い**1、2文で、インシデントの原因や、タイムライン、および影響などを要約します。
たとえば「8月9日の朝、プライマリデータベースマシンの暴走により1分間のSEV-1が発生しました。この遅延により、0.024%のPagerDutyアラートがSLA違反となりました。」_

## 何が起こったか

_何が起こったかを簡潔に書く_

## 根本原因

_問題を引き起こした全ての条件を書く。問題を悪化させるようなアクションをしても、対応中に犯したミスから学ぶために全て書く。_

## 解決

_何によって問題が解決したか書く。一時的な措置を施した場合は、長期的な対策と共に書く。_

## 影響

_具体的な数字で正確に書く_

|                                     |                                                |
| -                                   | -                                              |
| SEV-1の時間                         | ?分                                          |
| SEV-2の時間                         | ?分                                          |
| SLA違反となった通知                 | ??% (?? 中 ??)                                 |
| 破棄された/処理されなかったイベント | ??% (?? 中 ??) _通常は0であるべきだが確認する_ |
| 影響を受けたアカウント              | ??                                             |
| 影響を受けたユーザー数              | ??                                             |
| 発生したサポートリクエスト          | ?? _関連するチケットへのリンク_                |

## 対応者

* _インシデントコマンダーはだれか？_
* _補佐は誰か？_
* _他に誰が関わったか？_

## タイムライン

_重要な時刻を書く。(1) 原因が発生した時刻、 (2) ページされた時刻、 (3) ステータスページが更新された時刻（つまり外部告知された時刻）、(4) 重要なアクションを実行した時刻、(5) SEV2/SEV-1が終わった時刻、(6) タイムスタンプが取得されたツール、ログへのリンク_

| Time (UTC) | Event | Data Link |
| ---------- | ----- | --------- |

## どうだったか？

### うまくいったこと

* _あなたがうまくいったと思ったことや、書きたいことをリストにします。全てを挙げなくても大丈夫です。_

### うまくいかなかったこと

* _あなたがうまくいかなかったと思ったことをリストにします。その目的は、プロセスを改善して全ての点でフォローアップするためです。_

## アクションアイテム

_各アクションアイテムはJIRAチケットの形式で、それぞれのチケットは "sev1_YYYYMMDD" と "sev1" のタグを持ちます。
アクションアイテムは (1) 再発防止のための修正、(2) 問題が再発しても問題が小さくなるような措置、 (3) 内部メールやステータスページの更新などのポストモーテムの残り作業、 (4) インシデント対応プロセスの改善、などです。_

## メッセージ

### 内部メール

_従業員に対するフォローアップです。ポストモーテムミーティングが終わった後すぐに送るべきです。メールにはインシデントの簡単な説明とwikiへのリンクを貼ります_

> 何が起こったか、ポストモーテムへのページがどこにあるかを、簡単に要約します

### 外部告知

_インシデントに関してstatus.pagerduty.comに掲載することです。顧客に何を伝えて、どう謝罪しますか？（謝罪は定型文ではなく真摯に書くべきです）_

> 概要

> 何が起こったか

> これに対して私たちは何をしている

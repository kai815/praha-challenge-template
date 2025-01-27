```uml
@startuml
object 参加者 {
  id
  名前
  メールアドレス
  在籍ステータス
}

note right of (参加者)
・メールアドレスの重複は許容されない
・ステータスが「在籍中」以外の場合、
  どのチームにもペアにも所属してはいけない
end note

object ペア{
  id
  名前
}

note right of (ペア)
・名前はa,b,c,d,eのような英文字でなければいけない
・名前は1文字でなければならない
・参加者は2名〜3名まで。1名のペアや、4名のペアは存在できない
・ペアは必ず同じチームの参加者から選ばれます
end note

object ペアメンバー {
  id
  ペアID
  参加者ID
}

ペア "1" *-- "0...n" ペアメンバー
ペアメンバー "0...n" --> 参加者

object チーム {
  id
  名前
}

note right of (チーム)
・1,2,3,4のような数字でなければいけない。重複不可
・名前は3文字以下でなければいけない（チーム1031は存在できない。999まで）
・最低でも参加者が3名いなければならない。
end note

object チームメンバー {
  id
  チームID
  参加者ID
}

チーム "1" *-- "0...n" チームメンバー
チームメンバー "0...n" --> 参加者


object 課題 {
  id
  タイトル
  学ばないと何が起こるか
  説明
}

note right of (課題)
・全ての参加者は複数の課題（80個ぐらい）を所有（割り当てられて）いる
・進捗ステータスは「未着手、レビュー待ち、完了」いずれかの値を持つ
・進捗ステータスはいつでも変更可能
・ただし一度「完了」にした進捗ステータスを「レビュー待ち」「未着手」に戻すことはできない
・進捗ステータスを変更できるのは、
  課題の所有者だけ（Aさんの課題1の進捗ステータスを変えられるのはAさんだけ。Aさんの課題1の進捗ステータスをBさんが変更するのは不可能）
end note

object 参加者課題 {
  id
  課題ID
  参加者ID
  進捗ステータス
}

課題 "1" *-- "0...n" 参加者課題
参加者課題 "0...n" --> 参加者

@enduml
```

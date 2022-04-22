```uml
@startuml

skinparam class {
    '図の背景
    BackgroundColor Snow
    '図の枠
    BorderColor Black
    'リレーションの色
    ArrowColor Black
}

!define MASTER_MARK_COLOR Orange 
!define TRANSACTION_MARK_COLOR DeepSkyBlue

package "ECサイト" as target_system {
    /'
      マスターテーブルを M、トランザクションを T などで表記
      １文字なら "主" とか "従" まど日本語でも記載可能
     '/

    entity "参加者マスタ" as customer <m_customers> <<M,MASTER_MARK_COLOR>> {
        + cu_id [PK]
        --
        cu_name
        cu_age
        cu_status
        cu_sei
        cu_user
        cu_mail
        cu_pass
    }
    
    entity "企業マスタ" as order <order> <<M,MASTER_MARK_COLOR>> {
        + co_id [PK]
        --
        co_name
        co_place
        co_hp
        co_user
        co_pass
    }
    
    entity "ボランティア一覧テーブル" as volunteer  <volunteer> <<T,TRANSACTION_MARK_COLOR>> {
        + v_id[PK]
        --
        v_name
        v_place1
        v_place2
        v_info
        v_comp
        v_day
        v_people
    }
    
     entity "ボランティア一覧の画像テーブル" as volunteer_pic  <volunteer_pic> <<T,TRANSACTION_MARK_COLOR>> {
        + id[PK]
        --
        img
        img_name
        user_name
    }
    
    entity "参加済みマスタ" as join <join> <<M,MASTER_MARK_COLOR>> {
        + j_id [PK]
        --
        j_name
        j_place1
        j_place2
        j_info
        j_comp
        j_day
    }
    
    entity "開発者マスタ" as developer <developer> <<M,MASTER_MARK_COLOR>> {
        + co_id [PK]
        --
        co_name
        co_user
        co_pass
    }
  }
  
  customer       |o-ri-o{     order
order          ||-ri-|{     volunteer
volunteer          ||-ri-|{  volunteer_pic
volunteer  }-do-||     join
join          }o-le-||     developer


@enduml
```


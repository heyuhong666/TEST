```mermaid
flowchart TD
    %% 
    CSW1["CSW1 (AX2340S-24P4X)"]

    %% HUB
    KIKI["機器HUB (ELECOM)"]
    PCHUB["PC-HUB (ELECOM)"]
    CAMHUB["防犯カメラHUB (ELECOM)"]
    REJIHUB1["レジHUB1 (ELECOM)"]
    REJIHUB2["レジHUB2 (ELECOM)"]
    SCHUB["SCHUB (ELECOM)"]
    RSW1A1["RSW1A1 (AX2340S-24P4X)"]

    %% CSW1 上联
    CSW1 --- KIKI
    CSW1 --- PCHUB
    CSW1 --- CAMHUB
    CSW1 --- REJIHUB1
    CSW1 --- REJIHUB2
    CSW1 --- SCHUB
    CSW1 --- RSW1A1

    %% 機器HUB 末端
    KIKI --- 打刻機
    KIKI --- 複合機
    KIKI --- フクシマ
    KIKI --- 青果作業場
    KIKI --- 精肉作業場
    KIKI --- 惣菜作業場
    KIKI --- 電子棚札

    %% PC-HUB 末端
    PCHUB --- PC201
    PCHUB --- PC202
    PCHUB --- PC203
    PCHUB --- PC204

    %% 防犯カメラHUB
    CAMHUB --- 防犯カメラ1
    CAMHUB --- 防犯カメラ2
    CAMHUB --- 防犯カメラ3
    CAMHUB --- 防犯カメラ4

    %% レジHUB1
    REJIHUB1 --- レジ機1
    REJIHUB1 --- レジ機2
    REJIHUB1 --- レジ機3
    REJIHUB1 --- レジ機4
    REJIHUB1 --- レジ機5
    REJIHUB1 --- レジ機6
    REJIHUB1 --- レジ機7

    %% レジHUB2
    REJIHUB2 --- レジ機8
    REJIHUB2 --- レジ機9
    REJIHUB2 --- レジ機10
    REJIHUB2 --- レジ機11
    REJIHUB2 --- レジ機12
    REJIHUB2 --- レジ機13
    REJIHUB2 --- レジ機14

    %% SCHUB
    SCHUB --- SCレジ1
    SCHUB --- SCレジ2
    SCHUB --- PC207
    SCHUB --- 現金管理機
    SCHUB --- 現金管理カメラ

    %% RSW1A1
    RSW1A1 --- AP109
    RSW1A1 --- AP110
    RSW1A1 --- AP111

    %% CSW1 
    CSW1 --- 事務機
    CSW1 --- ドラッグレジ
    CSW1 --- ドラッグPC
    CSW1 --- カメラSV
    CSW1 --- サイネージSV
    CSW1 --- AP101
    CSW1 --- AP102
    CSW1 --- AP103
    CSW1 --- AP104
    CSW1 --- AP105
    CSW1 --- AP106
    CSW1 --- AP107
    CSW1 --- AP108
    CSW1 --- AP112

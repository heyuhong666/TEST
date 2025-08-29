```mermaid
flowchart TD
    %% coreSW
    CSW1["CSW1 (AX2340S-24P4X)"]

    %% HUB / SW
    KIKI["機器HUB (ELECOM)"]
    PCHUB["PC-HUB (ELECOM)"]
    CAMHUB["防犯カメラHUB (ELECOM)"]
    REJIHUB1["レジHUB1 (ELECOM)"]
    REJIHUB2["レジHUB2 (ELECOM)"]
    SCHUB["SCHUB (ELECOM)"]
    RSW1A1["RSW1A1 (AX2340S-24P4X)"]

    %% CSW1 
    CSW1 --- 機器HUB
    CSW1 --- PCHUB
    CSW1 --- CAMHUB
    CSW1 --- REJIHUB1
    CSW1 --- REJIHUB2
    CSW1 --- SCHUB
    CSW1 --- RSW1A1

# 台灣社群非官方 Ubuntu 虛擬機器<br/>Ubuntu-TW-VM
<https://github.com/Ubuntu-Taiwan-Community/Ubuntu-TW-VM>

## 簡介<br>Introduction
「台灣社群非官方 Ubuntu 虛擬機器」為基於「ubuntu 作業系統」所開發的 virtual appliance（虛擬應用裝置），其開發宗旨為：

* 提供需要 ubuntu 虛擬機器的使用者一個設定好可以直接使用的基本中文操作環境
* 作為「台灣社群非官方客製版 ubuntu 作業系統」的實現經驗累積

本軟體包含：

* 截至釋出時刻的最新版本軟體
* 堪用的中文輸入法（僅將 Ubuntu 預設提供的輸入法框架設定到可正常輸入中文為止）
* Oracle Virtualbox 與 VMware Workstation 客端支援軟體（設定到可以讓畫面自動適應虛擬機器視窗大小以及支援將 3D 繪圖運算卸載到主端硬體）
* 設定過程中所需要安裝的額外軟體，包含但不限於 GNU Gparted 跟 zerofree
* ubuntu-restricted-extras ubuntu 受限制軟體集合

本軟體不包含：

* 一個完整可佈署到實體機器上的系統安裝程式與媒體（這屬於「台灣社群非官方客製版 ubuntu 作業系統」的範疇）
* 完整的中文化支援修正（包含但不限於 TTY 終端機中文支援）（這也屬於「台灣社群非官方客製版 ubuntu 作業系統」的範疇）
* 自動化系統建構程式，這邊釋出的版本皆為人工建構不保證完整性（這一樣也屬於「台灣社群非官方客製版 ubuntu 作業系統」的範疇）

一言以蔽之，這是一個因為「台灣社群非官方客製版 ubuntu 作業系統」目前還不夠完善所以產生出來的妥協品，讓你可以不用自己從頭設定一個 ubuntu 虛擬機器。

## 智慧財產授權條款<br>Intellectual Property License
本軟體由無數個子軟體所共同組成，請參考各軟體安裝於 `/usr/share/doc/*/LICENSE` 位置的授權條款。

注意本軟體亦基於合理使用(fair use)原則下包含非屬於自由軟體定義下授權授權條款或被軟體專利所限制的軟體，包含但不限於：

* ubuntu-restricted-extras 軟體包所包含的軟體，包含但不限於：
	* Adobe Flash Player（專有軟體、免費軟體）
	* Microsoft [Core fonts for the Web](https://en.wikipedia.org/wiki/Core_fonts_for_the_Web)（免費軟體）
	* 部份多媒體編碼器與解碼器（含受專利限制軟體、免費軟體）
	* RAR 封存檔之壓縮與解壓縮程式（受專利限制軟體、免費軟體（解壓縮程式）、試用付費軟體（壓縮程式））

使用本軟體視同同意遵從這些軟體之授權條款與專利限制細節，本專案不負擔任何使用本軟體所衍伸之法律責任並拋棄本軟體的所有權至公有領域(Public Domain)。

## 取得軟體<br>Acquire Software
請至本專案的[軟體釋出頁面](https://github.com/Ubuntu-Taiwan-Community/Ubuntu-TW-VM/releases)下載軟體，並請留意軟體的釋出說明。

## 已知問題與解決方案<br>Known Issues & Solutions
### VMware 在匯入 Open Virtualization Format(OVF) 格式的 virtual appliance（虛擬應用裝置）時回報下列錯誤：「The import failed because 〈虛擬應用裝置封存檔〉 did not pass OVF specification conformance or virtual hardware compliance checks.  Click Retry to relax OVF specification and virtual hardware compliance checks and try the import again, or click Cancel to cancel the import. If you retry the import, you might not be able to use the virtual machine in VMware Player.  [<u>C</u>ancel] [<u>R</u>etry]」

#### 原因
可能是 VirtualBox 產生的 OVF 格式並不完全相容 VMware，或是不完全遵從 OVF 的規範：

```
Error: OVF Package is not supported by target:
 - Line 67: Unsupported hardware family 'virtualbox-2.2'.
```

#### 解決方案
點擊 [<u>R</u>etry] 即可讓 VMware 放寬限制匯入虛擬應用裝置

### 在 VMware 虛擬化解決方案中不支援硬體 3D 繪圖工作卸載，造成圖形界面操作反應遲緩
#### 原因
這是因為 VMware 預設將主端使用之開放來源碼 Mesa 3D 驅動列為黑名單預設不使用導致

#### 解決方案
在虛擬機器的 VMX 檔案中加入：

    mks.gl.allowBlacklistedDrivers = "TRUE"

#### 參考資料
[virtualization - How to fix 3D Acceleration for Vmware Workstation 9? - Ask Ubuntu](http://askubuntu.com/questions/181829/how-to-fix-3d-acceleration-for-vmware-workstation-9)

PowerCLI
----

Windows Powershellから実行できるCLI環境。

### 利用方法

1. デスクトップアイコンをダブルクリックして起動（Powershell上でコマンドを叩いて起動、ではない）。
1. `Connect-VIServer`コマンドでvCenterサーバーへ接続。
  対話式に接続されるため引数、オプションは不要。
1. 目的のコマンドを実行。

### 主要なコマンド

* `Get-VM` : 仮想マシンの情報を取得する。

### スニペット

特定ESXi上の稼働中VMを一覧化する。

```powershell
Get-VM | where {$_.VMHost -match 'esxiname' -and $_.PowerState -match 'PoweredOn'} | select Name,VMHost,PowerState
```
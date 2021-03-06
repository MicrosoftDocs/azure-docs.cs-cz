---
title: Rychlý Start Azure Cloud Shell – PowerShell
description: Naučte se používat PowerShell v prohlížeči s Azure Cloud Shell.
author: maertendmsft
ms.author: damaerte
tags: azure-resource-manager
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 10/18/2018
ms.openlocfilehash: d4a7f1453ec686cfa16d260101ba81f429ce1da0
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/09/2020
ms.locfileid: "89469452"
---
# <a name="quickstart-for-powershell-in-azure-cloud-shell"></a>Rychlý Start pro PowerShell v Azure Cloud Shell

Tento dokument popisuje, jak používat PowerShell v Cloud Shell v [Azure Portal](https://portal.azure.com/).

> [!NOTE]
> K dispozici je také [bash v Azure Cloud Shell](quickstart.md) rychlý Start.

## <a name="start-cloud-shell"></a>Spuštění Cloud Shellu

1. V horním navigačním panelu Azure Portal klikněte na tlačítko **Cloud Shell**

   ![Snímek obrazovky znázorňující, jak začít Azure Cloud Shell z Azure Portal](media/quickstart-powershell/shell-icon.png)

2. V rozevíracím seznamu vyberte prostředí PowerShell a budete na jednotce Azure. `(Azure:)`

   ![Snímek obrazovky znázorňující, jak vybrat prostředí PowerShell pro Azure Cloud Shell.](media/quickstart-powershell/environment-ps.png)

## <a name="run-powershell-commands"></a>Spuštění příkazů PowerShellu

V Cloud Shell spouštějte běžné příkazy PowerShellu, například:

```azurepowershell-interactive
PS Azure:\> Get-Date

# Expected Output
Friday, July 27, 2018 7:08:48 AM

PS Azure:\> Get-AzVM -Status

# Expected Output
ResourceGroupName       Name       Location                VmSize   OsType     ProvisioningState  PowerState
-----------------       ----       --------                ------   ------     -----------------  ----------
MyResourceGroup2        Demo        westus         Standard_DS1_v2  Windows    Succeeded           running
MyResourceGroup         MyVM1       eastus            Standard_DS1  Windows    Succeeded           running
MyResourceGroup         MyVM2       eastus   Standard_DS2_v2_Promo  Windows    Succeeded           deallocated
```

## <a name="navigate-azure-resources"></a>Navigace v prostředcích Azure

 1. Zobrazit seznam všech předplatných z `Azure` jednotky

    ```azurepowershell-interactive
    PS Azure:\> dir
    ```

 2. `cd` do preferovaného předplatného

    ```azurepowershell-interactive
    PS Azure:\> cd MySubscriptionName
    PS Azure:\MySubscriptionName>
    ```

 3. Zobrazit všechny prostředky Azure v rámci aktuálního předplatného

    Zadejte `dir` , chcete-li zobrazit seznam více zobrazení prostředků Azure.

    ```azurepowershell-interactive
    PS Azure:\MySubscriptionName> dir

        Directory: azure:\MySubscriptionName

    Mode Name
    ---- ----
    +    AllResources
    +    ResourceGroups
    +    StorageAccounts
    +    VirtualMachines
    +    WebApps
    ```

### <a name="allresources-view"></a>Zobrazení AllResources

Zadejte do pole `dir` `AllResources` adresář, aby se zobrazily prostředky Azure.

```azurepowershell-interactive
PS Azure:\MySubscriptionName> dir AllResources
```

### <a name="explore-resource-groups"></a>Prozkoumat skupiny prostředků

 Můžete přejít do `ResourceGroups` adresáře a uvnitř konkrétní skupiny prostředků, kde můžete najít virtuální počítače.

```azurepowershell-interactive
PS Azure:\MySubscriptionName> cd ResourceGroups\MyResourceGroup1\Microsoft.Compute\virtualMachines

PS Azure:\MySubscriptionName\ResourceGroups\MyResourceGroup1\Microsoft.Compute\virtualMachines> dir


    Directory: Azure:\MySubscriptionName\ResourceGroups\MyResourceGroup1\Microsoft.Compute\virtualMachines


VMName    Location   ProvisioningState VMSize          OS            SKU             OSVersion AdminUserName  NetworkInterfaceName
------    --------   ----------------- ------          --            ---             --------- -------------  --------------------
TestVm1   westus     Succeeded         Standard_DS2_v2 WindowsServer 2016-Datacenter Latest    AdminUser      demo371
TestVm2   westus     Succeeded         Standard_DS1_v2 WindowsServer 2016-Datacenter Latest    AdminUser      demo271
```

> [!NOTE]
> Můžete si všimnout, že při psaní podruhé `dir` je Cloud Shell možné zobrazit položky mnohem rychleji.
> Je to proto, že podřízené položky jsou ukládány do mezipaměti v paměti pro lepší činnost koncového uživatele.
Můžete ale kdykoli použít `dir -Force` k získání nových dat.

### <a name="navigate-storage-resources"></a>Navigace v prostředcích úložiště

Když do adresáře zadáte `StorageAccounts` , můžete snadno procházet všechny prostředky úložiště.

```azurepowershell-interactive
PS Azure:\MySubscriptionName\StorageAccounts\MyStorageAccountName\Files> dir

    Directory: Azure:\MySubscriptionNameStorageAccounts\MyStorageAccountName\Files

Name          ConnectionString
----          ----------------
MyFileShare1  \\MyStorageAccountName.file.core.windows.net\MyFileShare1;AccountName=MyStorageAccountName AccountKey=<key>
MyFileShare2  \\MyStorageAccountName.file.core.windows.net\MyFileShare2;AccountName=MyStorageAccountName AccountKey=<key>
MyFileShare3  \\MyStorageAccountName.file.core.windows.net\MyFileShare3;AccountName=MyStorageAccountName AccountKey=<key>
```

Pomocí připojovacího řetězce můžete připojit sdílenou složku souborů Azure pomocí následujícího příkazu.

```azurepowershell-interactive
net use <DesiredDriveLetter>: \\<MyStorageAccountName>.file.core.windows.net\<MyFileShareName> <AccountKey> /user:Azure\<MyStorageAccountName>
```

Podrobnosti najdete v tématu [připojení sdílené složky Azure Files a přístup ke sdílené složce v systému Windows][azmount].

Adresáře ve sdílené složce služby soubory Azure můžete také procházet následujícím způsobem:

```azurepowershell-interactive
PS Azure:\MySubscriptionName\StorageAccounts\MyStorageAccountName\Files> cd .\MyFileShare1\
PS Azure:\MySubscriptionName\StorageAccounts\MyStorageAccountName\Files\MyFileShare1> dir

Mode  Name
----  ----
+     TestFolder
.     hello.ps1
```

### <a name="interact-with-virtual-machines"></a>Interakce s virtuálními počítači

Všechny virtuální počítače můžete najít v rámci aktuálního předplatného prostřednictvím `VirtualMachines` adresáře.

```azurepowershell-interactive
PS Azure:\MySubscriptionName\VirtualMachines> dir

    Directory: Azure:\MySubscriptionName\VirtualMachines


Name       ResourceGroupName  Location  VmSize          OsType              NIC ProvisioningState  PowerState
----       -----------------  --------  ------          ------              --- -----------------  ----------
TestVm1    MyResourceGroup1   westus    Standard_DS2_v2 Windows       my2008r213         Succeeded     stopped
TestVm2    MyResourceGroup1   westus    Standard_DS1_v2 Windows          jpstest         Succeeded deallocated
TestVm10   MyResourceGroup2   eastus    Standard_DS1_v2 Windows           mytest         Succeeded     running
```

#### <a name="invoke-powershell-script-across-remote-vms"></a>Vyvolání skriptu PowerShellu napříč vzdálenými virtuálními počítači

 > [!WARNING]
 > Přečtěte si prosím [řešení potíží se vzdálenou správou virtuálních počítačů Azure](troubleshooting.md#troubleshooting-remote-management-of-azure-vms).

  Za předpokladu, že máte virtuální počítač, MyVM1, využijeme `Invoke-AzVMCommand` k vyvolání bloku skriptu PowerShellu na vzdáleném počítači.

  ```azurepowershell-interactive
  Enable-AzVMPSRemoting -Name MyVM1 -ResourceGroupname MyResourceGroup
  Invoke-AzVMCommand -Name MyVM1 -ResourceGroupName MyResourceGroup -Scriptblock {Get-ComputerInfo} -Credential (Get-Credential)
  ```

  Můžete také nejprve přejít do adresáře VirtualMachines a spustit ho `Invoke-AzVMCommand` následujícím způsobem.

  ```azurepowershell-interactive
  PS Azure:\> cd MySubscriptionName\ResourceGroups\MyResourceGroup\Microsoft.Compute\virtualMachines
  PS Azure:\MySubscriptionName\ResourceGroups\MyResourceGroup\Microsoft.Compute\virtualMachines> Get-Item MyVM1 | Invoke-AzVMCommand -Scriptblock {Get-ComputerInfo} -Credential (Get-Credential)

  # You will see output similar to the following:

  PSComputerName                                          : 65.52.28.207
  RunspaceId                                              : 2c2b60da-f9b9-4f42-a282-93316cb06fe1
  WindowsBuildLabEx                                       : 14393.1066.amd64fre.rs1_release_sec.170327-1835
  WindowsCurrentVersion                                   : 6.3
  WindowsEditionId                                        : ServerDatacenter
  WindowsInstallationType                                 : Server
  WindowsInstallDateFromRegistry                          : 5/18/2017 11:26:08 PM
  WindowsProductId                                        : 00376-40000-00000-AA947
  WindowsProductName                                      : Windows Server 2016 Datacenter
  WindowsRegisteredOrganization                           :
   ...
  ```

#### <a name="interactively-log-on-to-a-remote-vm"></a>Interaktivní přihlášení ke vzdálenému virtuálnímu počítači

Můžete použít `Enter-AzVM` k interaktivnímu přihlášení k virtuálnímu počítači běžícímu v Azure.

  ```azurepowershell-interactive
  PS Azure:\> Enter-AzVM -Name MyVM1 -ResourceGroupName MyResourceGroup -Credential (Get-Credential)
  ```

Můžete také přejít k `VirtualMachines` adresáři jako první a spustit `Enter-AzVM` následujícím způsobem.

  ```azurepowershell-interactive
 PS Azure:\MySubscriptionName\ResourceGroups\MyResourceGroup\Microsoft.Compute\virtualMachines> Get-Item MyVM1 | Enter-AzVM -Credential (Get-Credential)
 ```

### <a name="discover-webapps"></a>Zjistit WebApps

Když zadáte do `WebApps` adresáře, můžete snadno procházet prostředky webových aplikací.

```azurepowershell-interactive
PS Azure:\MySubscriptionName> dir .\WebApps\

    Directory: Azure:\MySubscriptionName\WebApps

Name            State    ResourceGroup      EnabledHostNames                  Location
----            -----    -------------      ----------------                  --------
mywebapp1       Stopped  MyResourceGroup1   {mywebapp1.azurewebsites.net...   West US
mywebapp2       Running  MyResourceGroup2   {mywebapp2.azurewebsites.net...   West Europe
mywebapp3       Running  MyResourceGroup3   {mywebapp3.azurewebsites.net...   South Central US

# You can use Azure cmdlets to Start/Stop your web apps
PS Azure:\MySubscriptionName\WebApps> Start-AzWebApp -Name mywebapp1 -ResourceGroupName MyResourceGroup1

Name           State    ResourceGroup        EnabledHostNames                   Location
----           -----    -------------        ----------------                   --------
mywebapp1      Running  MyResourceGroup1     {mywebapp1.azurewebsites.net ...   West US

# Refresh the current state with -Force
PS Azure:\MySubscriptionName\WebApps> dir -Force

    Directory: Azure:\MySubscriptionName\WebApps

Name            State    ResourceGroup      EnabledHostNames                  Location
----            -----    -------------      ----------------                  --------
mywebapp1       Running  MyResourceGroup1   {mywebapp1.azurewebsites.net...   West US
mywebapp2       Running  MyResourceGroup2   {mywebapp2.azurewebsites.net...   West Europe
mywebapp3       Running  MyResourceGroup3   {mywebapp3.azurewebsites.net...   South Central US
```

## <a name="ssh"></a>SSH

Chcete-li provést ověření na serverech nebo virtuálních počítačích pomocí protokolu SSH, vygenerujte dvojici klíčů veřejného a privátního klíče v Cloud Shell a publikujte veřejný klíč na `authorized_keys` vzdáleném počítači, například `/home/user/.ssh/authorized_keys` .

> [!NOTE]
> Privátní veřejné klíče SSH můžete vytvořit pomocí `ssh-keygen` a publikovat je `$env:USERPROFILE\.ssh` v nástroji v Cloud Shell.

### <a name="using-ssh"></a>Použití SSH

Pokud chcete vytvořit novou konfiguraci virtuálního počítače pomocí rutin [Azure PowerShell, postupujte](../virtual-machines/linux/quick-create-powershell.md) podle pokynů.
Než zahájíte volání do `New-AzVM` nasazení, přidejte do konfigurace virtuálního počítače veřejný klíč SSH.
Nově vytvořený virtuální počítač bude obsahovat veřejný klíč v `~\.ssh\authorized_keys` umístění, čímž se k virtuálnímu počítači zapíná relace SSH bez přihlašovacích údajů.

```azurepowershell-interactive
# Create VM config object - $vmConfig using instructions on linked page above

# Generate SSH keys in Cloud Shell
ssh-keygen -t rsa -b 2048 -f $HOME\.ssh\id_rsa 

# Ensure VM config is updated with SSH keys
$sshPublicKey = Get-Content "$HOME\.ssh\id_rsa.pub"
Add-AzVMSshPublicKey -VM $vmConfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"

# Create a virtual machine
New-AzVM -ResourceGroupName <yourResourceGroup> -Location <vmLocation> -VM $vmConfig

# SSH to the VM
ssh azureuser@MyVM.Domain.Com
```

## <a name="list-available-commands"></a>Zobrazit dostupné příkazy

V části `Azure` jednotka zadejte, `Get-AzCommand` aby se získaly příkazy Azure specifické pro kontext.

Případně můžete k `Get-Command *az* -Module Az.*` Získání dostupných příkazů Azure vždycky použít.

## <a name="install-custom-modules"></a>Nainstalovat vlastní moduly

Můžete spustit `Install-Module` pro instalaci modulů z [Galerie prostředí PowerShell][gallery].

## <a name="get-help"></a>Get-Help

Zadejte `Get-Help` , chcete-li získat informace o PowerShellu v Azure Cloud Shell.

```azurepowershell-interactive
Get-Help
```

U určitého příkazu můžete i nadále používat `Get-Help` rutinu.

```azurepowershell-interactive
Get-Help Get-AzVM
```

## <a name="use-azure-files-to-store-your-data"></a>Použití souborů Azure k ukládání dat

Můžete vytvořit skript, říkáte `helloworld.ps1` ho a uložte ho do souboru, `clouddrive` abyste ho mohli použít napříč relacemi prostředí.

```azurepowershell-interactive
cd $HOME\clouddrive
# Create a new file in clouddrive directory
New-Item helloworld.ps1
# Open the new file for editing
code .\helloworld.ps1
# Add the content, such as 'Hello World!'
.\helloworld.ps1
Hello World!
```

Když použijete PowerShell v Cloud Shell, `helloworld.ps1` soubor bude existovat v `$HOME\clouddrive` adresáři, který je připojen ke sdílené složce Azure Files.

## <a name="use-custom-profile"></a>Použít vlastní profil

Prostředí PowerShell můžete přizpůsobit vytvořením profilů PowerShellu – `profile.ps1` (nebo `Microsoft.PowerShell_profile.ps1` ).
Uložte ji pod `$profile.CurrentUserAllHosts` (nebo `$profile.CurrentUserAllHosts` ), aby se mohla načíst do každého PowerShellu v Cloud Shell relace.

Informace o tom, jak vytvořit profil, najdete v tématu [o profilech][profile].

## <a name="use-git"></a>Použití Gitu

K naklonování úložiště Git v Cloud Shell musíte vytvořit [osobní přístupový token][githubtoken] a použít ho jako uživatelské jméno. Jakmile budete mít token, naklonujte úložiště následujícím způsobem:

```azurepowershell-interactive
  git clone https://<your-access-token>@github.com/username/repo.git
```

## <a name="exit-the-shell"></a>Opusťte prostředí

Zadejte `exit` , chcete-li ukončit relaci.

[bashqs]:quickstart.md
[gallery]:https://www.powershellgallery.com/
[customex]:https://docs.microsoft.com/azure/virtual-machines/windows/extensions-customscript
[profile]: /powershell/module/microsoft.powershell.core/about/about_profiles
[azmount]: ../storage/files/storage-how-to-use-files-windows.md
[githubtoken]: https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/
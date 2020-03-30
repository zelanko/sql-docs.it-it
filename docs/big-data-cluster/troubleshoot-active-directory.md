---
title: Risolvere i problemi di distribuzione in modalità Active Directory
titleSuffix: SQL Server Big Data Cluster
description: Risolvere i problemi di distribuzione di un cluster Big Data di SQL Server in un dominio di Active Directory.
author: rl-msft
ms.author: rafidl
ms.reviewer: mikeray
ms.date: 03/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d887eadd021641241516a1478c6ac13e0d0bdec
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "79191212"
---
# <a name="troubleshoot-sql-server-big-data-cluster-active-directory-mode-deployment"></a>Risolvere i problemi di distribuzione di un cluster Big Data di SQL Server in modalità Active Directory

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo illustra come risolvere i problemi di distribuzione di un cluster Big Data di SQL Server in modalità Active Directory.

## <a name="check-deployment-progress"></a>Controllare lo stato di avanzamento della distribuzione

Questa operazione può richiedere alcuni minuti. Se il cluster non è pronto dopo 15 minuti, controllare i log del controller per altri dettagli.

Durante la distribuzione del cluster, controllare i pod.

```console
kubectl get pods -n mssql-cluster
```

Verificare che l'elenco dei pod restituiti includa:

- `compute-`$
- `data-`
- `storage-`

Se i pod di calcolo, dati e archiviazione non vengono creati, controllare i log per individuare i motivi.

## <a name="check-logs"></a>Controllare i log

Per identificare il motivo per cui la distribuzione viene terminata senza creare pod di calcolo, dati o archiviazione, controllare i log seguenti: 

- Controllare `controller.log` (`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\control-<suffix>\controller\controller\<date>\controller.log`). Cercare la voce seguente:

  `WARN | StatefulSet master is not ready with 0 ready pods and 3 unready pods `

- Controllare `master-0` `provisioner.log` (`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\master-0\mssql-server\provisioner\provisioner.log`)

  ```
  ERROR | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
    Traceback (most recent call last):
      File "/opt/provisioner/bin/scripts/provisioningpool.py", line 214, in executeNonQueries
        connection.execute_non_query(command)
      File "src/_mssql.pyx", line 1033, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1061, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1634, in _mssql.check_and_raise
      File "src/_mssql.pyx", line 1683, in _mssql.maybe_raise_MSSQLDatabaseException
    _mssql.MSSQLDatabaseException: (15401, b"Windows NT user or group '<domain>.<top-level-domain>\\<domain-group>' not found. Check the name again.DB-Lib error message 20018, severity 16:\nGeneral SQL Server error: Check messages from the SQL Server\n")
  WARNING | [3/3] Provisioning exception occurred during provisioning step: ProvisioningMasterPool.
  WARNING | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
  WARNING | Retrying.
  ```

  Nell'esempio precedente la distribuzione non riesce a creare un account di accesso per l'utente di dominio perché l'ambito del gruppo di dominio è locale al dominio. Usare gruppi con ambito globale o universale di dominio. In [Distribuire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] in modalità Active Directory](deploy-active-directory.md) vengono presentati i requisiti per l'ambito dei gruppi di AD.

## <a name="check-the-scope-of-domain-groups"></a>Controllare l'ambito dei gruppi di dominio.

Controllare l'ambito del gruppo di dominio (<`domain-group`>). Usare [get-adgroup](/powershell/module/addsadministration/get-adgroup/).

Se l'ambito del gruppo `<domain-group>` è locale al dominio (`DomainLocal`), la distribuzione non riesce. 

Lo script di PowerShell seguente controlla l'ambito di due gruppi di AD denominati `bdcadmins` e `bdcusers`. Sostituire i nomi con i nomi dei gruppi. 

```powershell
#Administrators and users AD groups
$Cluster_admins_group='bdcadmins'
$Cluster_users_group='bdcusers'

#Performing AD Group Checks...

#AD admin group Check
$ClusterAdminGroupScope_Result = New-Object System.Collections.ArrayList
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_admins_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterAdminGroupScope_Result.Add("Misconfiguration - $Cluster_admins_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal") 
    }
    else {
        [void]$ClusterAdminGroupScope_Result.Add("OK - $Cluster_admins_group Group scope is $GroupScope")
    }
}
catch {
    [void]$ClusterAdminGroupScope_Result.Add("Error - " + $_.exception.message)
}
#Ad users group check
$ClusterUsersGroupScope_Result = New-Object System.Collections.ArrayList
$GroupScope = ''
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_users_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterUsersGroupScope_Result.Add("Misconfiguration - $Cluster_users_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal")
    } 
    else 
    { [void]$ClusterUsersGroupScope_Result.Add("OK - $Cluster_users_group Group scope is $GroupScope") }
}
catch {
    [void]$ClusterUsersGroupScope_Result.Add("Error - " + $_.exception.message)
}

#Display the results
$ClusterUsersGroupScope_Result
```

## <a name="check-security-support-container"></a>Controllare il contenitore del supporto per la sicurezza 

Esaminare i log del contenitore del supporto per la sicurezza.

Il comando seguente raccoglie i log di supporto per la sicurezza in un cluster nello spazio dei nomi `mssql-cluster`.

```console
azdata bdc debug copy-logs -n mssql-cluster -c security-support
```

Estrarre i log e individuare `\mssql-cluster\control-<identifier>\controller\control-rts5t-controller-stdout.log`.

Cercare le voci seguenti nel log:

```
ERROR    | Failed to create AD user account 'cntrl-controller'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=cntrl-controller,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform. 
ERROR | Failed to create AD user account 'ldap-user'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=ldap-user,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform. 
ERROR | Failed to create AD user account 'nginx-mgmtproxy'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=nginx-mgmtproxy,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform.
```

Queste voci possono essere presenti quando nel server DNS del controller di dominio manca la voce DNS inversa (record PTR).

## <a name="verify-reverse-lookup-ptr-record"></a>Verificare la ricerca inversa (record PTR)
    
Eseguire lo script di PowerShell seguente per verificare se è stata configurata una voce DNS inversa (record PTR).

```powershell
#Domain Controller FQDN 'DCserver01.contoso.local'
$Domain_controller_FQDN = 'DCserver01.contoso.local'

#Performing Domain Controller DNS record, reverse PTR Checks...
$DcControllerDnsPtr_Result = New-Object System.Collections.ArrayList
try {
    $Domain_controller_DNS_Record = Resolve-DnsName $Domain_controller_FQDN -Type A -Server $Domain_DNS_IP_address -ErrorAction Stop
    foreach ($ip in $Domain_controller_DNS_Record.IPAddress) {
        #resolving hostname by IP address to make sure we have reverse PTR record 
        if ((Resolve-DnsName $ip).NameHost -eq $Domain_controller_FQDN) {
            [void]$DcControllerDnsPtr_Result.add("OK - $Domain_controller_FQDN has an A record with an IP $ip, Reverse PTR record is in place") 
        }
        else {
            [void]$DcControllerDnsPtr_Result.add("Missing - $Domain_controller_FQDN has an A record with an IP $ip, But no reverse PTR record was found for the host")
        }
    }
}
catch {
    [void]$DcControllerDnsPtr_Result.add("Error - " + $_.exception.message)
}

#show the results 
$DcControllerDnsPtr_Result
```

[Verificare la voce DNS inversa (record PTR) per il controller di dominio](deploy-active-directory.md#verify-reverse-dns-entry-for-domain-controller).
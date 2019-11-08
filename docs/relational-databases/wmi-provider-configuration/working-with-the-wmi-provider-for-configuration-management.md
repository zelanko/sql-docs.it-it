---
title: Usare il provider WMI per la gestione della configurazione
ms.custom: seo-lt-2019
ms.date: 04/12/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- WMI Provider for Configuration Management, connection strings
- WMI Provider for Configuration Management, security
- late binding [WMI]
- WMI Provider for Configuration Management, late binding
- binding [WMI]
ms.assetid: 34daa922-7074-41d0-9077-042bb18c222a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d76cc006e2f8638de9b6d3c21660806239022ec0
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/06/2019
ms.locfileid: "73657371"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>Utilizzo del provider WMI per Gestione configurazione

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Questo articolo fornisce indicazioni su come programmare con il provider WMI per la gestione dei computer.

## <a name="binding"></a>Associazione  
 Il provider WMI per Gestione configurazione è un modello a oggetti COM che supporta l'associazione anticipata e tardiva. Con l'associazione tardiva è possibile utilizzare linguaggi di scripting, come VBScript, per modificare a livello di codice gli alias, le impostazioni di rete e i servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="specifying-a-connection-string"></a>Definizione di una stringa di connessione

Le applicazioni indirizzano il provider WMI per Gestione configurazione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connettendosi a uno spazio dei nomi WMI definito dal provider. Il servizio Windows WMI esegue il mapping di questo spazio dei nomi alla DLL del provider e carica la DLL in memoria. Tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono rappresentate con un solo spazio dei nomi WMI.

Per impostazione predefinita, il formato dello spazio dei nomi è il seguente. Nel formato `VV` è il numero di versione principale di SQL Server. Il numero è individuabile eseguendo `SELECT @@VERSION;`.

```console
\\.\root\Microsoft\SqlServer\ComputerManagementVV
```

Quando si esegue la connessione tramite PowerShell, è necessario rimuovere la `\\.\` principale. Ad esempio, il codice PowerShell seguente elenca tutte le classi WMI per un SQL Server 2016, che è la versione principale 13.

```powershell
Get-WmiObject -Namespace 'root\Microsoft\SqlServer\ComputerManagement13' -List
```

<!--
Updated this on 2019-04-12, per:
   ~ https://github.com/MicrosoftDocs/sql-docs/issues/1817
   ~ https://github.com/rrg92/sql-docs/commit/3d518bfc0d55f819c762abc3e5c5c9eed85abe94?diff=unified

Thus from here I (GeneMi = MightyPen) removed the following text about 'instance_name':

'root\Microsoft\SqlServer\ComputerManagement13\instance_name'

where `instance_name` defaults to `MSSQLSERVER` in a default installation of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
-->

È possibile usare il codice PowerShell seguente per eseguire una query su tutti gli spazi dei nomi ComputerManagement WMI disponibili.

```powershell
gwmi -ns 'root\Microsoft\SqlServer' __NAMESPACE | ? {$_.name -match 'ComputerManagement' } | select name
```

 **Nota:** Se ci si connette tramite Windows Firewall sarà necessario assicurarsi che i computer siano configurati in modo appropriato. Vedere l'articolo "connessione tramite Windows Firewall" nella documentazione di Strumentazione gestione Windows su [!INCLUDE[msCoName](../../includes/msconame-md.md)] [sito Web](https://go.microsoft.com/fwlink/?linkid=15426)MSDN.  
  
## <a name="permissions-and-server-authentication"></a>Autorizzazioni e autenticazione del server  
 Per accedere al provider WMI per Gestione configurazione, è necessario che lo script di gestione WMI del client sia in esecuzione nel contesto di un amministratore nel computer di destinazione. È necessario essere membro del gruppo locale Administrators di Windows nel computer da gestire.  
  
 L'amministratore può impostare i criteri di gruppo per controllare l'accesso utente ai provider WMI. Per ulteriori informazioni sull'impostazione dei criteri di gruppo, vedere l'argomento relativo ai criteri di gruppo e a MMC nella Guida di Gestione configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Lo script di gestione WMI può essere utilizzato per aggiornare l'account con cui vengono eseguiti i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 I certificati di sicurezza sono supportati dal provider WMI per Gestione configurazione. Per ulteriori informazioni sui certificati, vedere [gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md)  
  
  

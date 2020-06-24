---
title: Accedere al provider WMI con VBScript
description: Informazioni su come creare un programma VBScript che elenca la versione delle istanze installate di SQL Server in esecuzione in un computer.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- VBScript [WMI]
- modifying SQL Server Service properties
- WMI Provider for Configuration Management, VBScript
ms.assetid: f3c5d981-eaa3-4d34-9b91-37e42636aa81
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fd515a60802f429611c1ae272216fac93642093e
ms.sourcegitcommit: bf5e9cb3a2caa25d0a37f401b3806b7baa5adea8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/24/2020
ms.locfileid: "85295454"
---
# <a name="access-wmi-provider-for-configuration-management-using-vbscript"></a>Accedere al provider WMI per Gestione configurazione con VBScript
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  In questa sezione viene descritto come creare un programma VBScript che elenca la versione delle istanze installate di in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esecuzione in un computer.  
  
 Nell'esempio di codice vengono elencate le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione nel computer e la relativa versione.  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>Elenco del nome e della versione delle istanze installate di SQL Server  
  
1.  Aprire un nuovo documento in un editor di testo, ad esempio Blocco note di [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Copiare il codice riportato dopo questa procedura e salvare il file con estensione vbs, ad esempio test.vbs.  
  
2.  Connettersi a un'istanza del provider WMI per Gestione computer con la funzione VBScript `GetObject`. In questo esempio viene effettuata la connessione a un computer remoto denominato mpc. Omettere il nome del computer per connettersi al computer locale: winmgmts:root\Microsoft\SqlServer\ComputerManagement. Per ulteriori informazioni sulla funzione `GetObject`, vedere l'argomento di riferimento per VBScript.  
  
3.  Utilizzare il metodo `InstancesOf` per enumerare un elenco dei servizi. È inoltre possibile enumerare i servizi mediante una query WQL semplice e il metodo `ExecQuery` anziché utilizzare il metodo `InstancesOf`.  
  
4.  Utilizzare il metodo `ExecQuery` e una query WQL per recuperare il nome e la versione delle istanze installate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  Salvare il file.  
  
6.  Eseguire lo script digitando **cscript test. vbs** al prompt dei comandi.  

## <a name="example"></a>Esempio  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  

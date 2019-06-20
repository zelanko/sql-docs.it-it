---
title: Modificare proprietà SQL Server Service avanzate utilizzando VBScript | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: f3a380f80b4ecc7540e29605543722edd55e226d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705062"
---
# <a name="modify-sql-server-service-advanced-properties-using-vbscript"></a>Modificare le proprietà avanzate del servizio SQL Server utilizzando VBScript
  In questa sezione viene descritto come creare un programma VBScript che elenca la versione delle istanze installate di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione in un computer.  
  
 Nell'esempio di codice vengono elencate le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione nel computer e la relativa versione.  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>Elenco del nome e della versione delle istanze installate di SQL Server  
  
1.  Aprire un nuovo documento in un editor di testo, ad esempio Blocco note di [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Copiare il codice riportato dopo questa procedura e salvare il file con estensione vbs, ad esempio test.vbs.  
  
2.  Connettersi a un'istanza del provider WMI per Gestione computer con la funzione VBScript `GetObject`. In questo esempio viene effettuata la connessione a un computer remoto denominato mpc. Omettere il nome del computer per connettersi al computer locale: winmgmts:root\Microsoft\SqlServer\ComputerManagement. Per ulteriori informazioni sulla funzione `GetObject`, vedere l'argomento di riferimento per VBScript.  
  
3.  Utilizzare il metodo `InstancesOf` per enumerare un elenco dei servizi. È inoltre possibile enumerare i servizi mediante una query WQL semplice e il metodo `ExecQuery` anziché utilizzare il metodo `InstancesOf`.  
  
4.  Utilizzare il metodo `ExecQuery` e una query WQL per recuperare il nome e la versione delle istanze installate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  Salvare il file.  
  
6.  Eseguire lo script digitando `cscript test.vbs` al prompt dei comandi.  
  
## <a name="example"></a>Esempio  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  

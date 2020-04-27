---
title: Installazione di preparazione aggiornamento dal prompt dei comandi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- command prompt [Upgrade Advisor]
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: a6841cc2-ca13-4b1c-9343-9e4d54312c3a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4b694af5b760ae3c1ead1e4984c35ef61c0fa602
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094340"
---
# <a name="installing-upgrade-advisor-from-the-command-prompt"></a>Installazione di Preparazione aggiornamento dal prompt dei comandi
  È possibile installare Preparazione aggiornamento utilizzando l'Installazione guidata o dal prompt dei comandi. Il prompt dei comandi consente di eseguire installazioni automatiche e automatizzate.  
  
## <a name="installation-syntax"></a>Sintassi dell'installazione  
 La sintassi di base per l'installazione di Preparazione aggiornamento dal prompt dei comandi è la seguente:  
  
 `SQLUA.msi [options]`  
  
 Nella tabella seguente vengono illustrate le opzioni più comuni.  
  
|Argomento|Descrizione|  
|--------------|-----------------|  
|/q [n&#124;b&#124;r&#124;f]|Imposta il livello dell'interfaccia utente:<br /><br /> n = nessuna interfaccia utente<br /><br /> b = interfaccia utente di base (solo stato di avanzamento, nessun prompt)<br /><br /> r = interfaccia utente ridotta (finestra di dialogo alla fine dell'installazione)<br /><br /> f = interfaccia utente completa|  
|/L|Specifica le opzioni del file di log. Per registrare tutti i messaggi in *log_file_name*, usare **-\*L v**_log_file_name_. Per registrare solo i messaggi di errore `-Le`, utilizzare *log_file_name*.|  
|ADDLOCAL = ALL&#124; REMOVE = ALL&#124;REINSTALL = ALL|Specifica se installare (ADDLOCAL), rimuovere (REMOVE) o reinstallare (REINSTALL) Preparazione aggiornamento.|  
|UAINSTALLDIR=path|Installa Preparazione aggiornamento nel percorso specificato da path.|  
  
## <a name="installation-examples"></a>Esempi dell'installazione  
 Nell'esempio seguente viene illustrato come installare Preparazione aggiornamento dal prompt dei comandi:  
  
```  
SQLUA.msi /qn ADDLOCAL=ALL UAINSTALLDIR="C:\Upgrade Advisor"  
```  
  
 È anche possibile utilizzare il programma Msiexec quando si esegue questo comando:  
  
```  
Msiexec.exe /i C:\Downloads\SQLUA.msi /qn ADDLOCAL=ALL UAINSTALLDIR="C:\Upgrade Advisor"  
```  
  
 Questa soluzione può risultare utile se è necessario utilizzare opzioni di installazione aggiuntive.  
  
## <a name="removal-examples"></a>Esempi di rimozione  
 Nell'esempio seguente viene illustrato come rimuovere Preparazione aggiornamento dal prompt dei comandi:  
  
```  
SQLUA.msi /qn REMOVE=ALL  
```  
  
 È anche possibile utilizzare il programma Msiexec quando si esegue questo comando:  
  
```  
Msiexec.exe /i C:\Downloads\SQLUA.msi /qn REMOVE=ALL  
```  
  
## <a name="see-also"></a>Vedi anche  
 [Installazione di preparazione aggiornamento](../../../2014/sql-server/install/installing-upgrade-advisor.md)   
 [Prerequisiti di Preparazione aggiornamento](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  

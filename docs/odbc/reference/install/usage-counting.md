---
title: Conteggio utilizzi | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca2a52eb08cdf1b1b9cb5a23805da34aab915b7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63273384"
---
# <a name="usage-counting"></a>Conteggio utilizzi
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows.  Solo nelle versioni precedenti di Windows è necessario installare ODBC in modo esplicito.  
  
 Due tipi di conteggi dell'utilizzo vengono mantenuti nel Registro di sistema per ogni componente: un conteggio di utilizzo del componente e uno o più conteggi dell'utilizzo di file facoltativa. Il conteggio di utilizzo del componente aiuta il programma di installazione DLL mantenere le voci del Registro di sistema. Viene archiviato nel valore UsageCount sotto la ODBC Core, driver e le sottochiavi di Microsoft translator. Per il formato del valore UsageCount e altre informazioni su queste sottochiavi, vedere [le voci del Registro di sistema per i componenti ODBC](../../../odbc/reference/install/registry-entries-for-odbc-components.md).  
  
 Quando un componente viene installato prima di tutto, il programma di installazione DLL creato una sottochiave e imposta i dati per il valore UsageCount nella sottochiave su 1. Quando il componente viene installato anche in questo caso, il programma di installazione DLL incrementa il conteggio di utilizzo. Quando il componente è stato rimosso, il programma di installazione DLL decrementa l'utilizzo di conteggio di. Se il conteggio di utilizzo scende a 0, il programma di installazione DLL rimuove la sottochiave del componente.  
  
> [!CAUTION]  
>  Un'applicazione non rimuovere fisicamente i file di Driver Manager quando il conteggio di utilizzo del componente e il conteggio di utilizzo file raggiunge zero.  
  
 Conteggi per determinare quando un file debba effettivamente essere copiato o eliminato come l'utilizzo di file anziché a incrementare o decrementare il conteggio di utilizzo. Questo è importante perché dei componenti ODBC e pertanto i file nei componenti ODBC, vengono condivisi e possono essere installati o rimosso da un'ampia gamma di applicazioni. L'applicazione può eliminare file di driver e di Microsoft translator se il conteggio di utilizzo del componente e il conteggio di utilizzo file raggiunge zero. File di Gestione driver non deve tuttavia, essere eliminati quando il conteggio di utilizzo del componente sia il conteggio di utilizzo di file hanno raggiunto lo zero, poiché questi file possono essere usati da altre applicazioni che non hanno incrementato il conteggio di utilizzo di file.  
  
> [!NOTE]  
>  Conteggi dell'utilizzo di file sono facoltativi in Microsoft® WindowsNT®/Windows 2000.  
  
 Conteggi dell'utilizzo di file vengono gestiti dal programma di installazione dopo avere chiamato **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLInstallTranslatorEx**, **SQLRemoveDriverManager**, **SQLRemoveDriver**, o **SQLRemoveTranslator**.  
  
 Quando un componente viene installato prima di tutto, il programma di installazione o il programma di installazione DLL crea un valore nella seguente chiave per ogni file in tale componente che non sia già nel sistema:  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  SOFTWARE  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  SharedDlls  
  
 Imposta i dati per i valori su 1 e copia il file di sistema. Quando il componente viene installato anche in questo caso, il programma di installazione o il programma di installazione DLL incrementa i conteggi dell'utilizzo. Quando il componente è stato rimosso, decrementa DLL programma o programma di installazione il programma di installazione il conteggio di utilizzo. Se qualsiasi numero di utilizzi scende a 0, il programma di installazione o di una DLL di installazione rimuove il valore per il file e, se il componente è un driver o una funzione di conversione, Elimina il file. I file di Gestione driver non devono essere eliminati.  
  
 Nella tabella seguente viene illustrato il formato del valore di conteggio dell'utilizzo del file.  
  
|Nome|Tipo di dati|Dati|  
|----------|---------------|----------|  
|*full-path*|REG_DWORD|*count*|  
  
 Ad esempio, si supponga che un driver per Informix Usa i file Infrmx32.dll e Infrmx32.hlp e si supponga che questo driver è stato installato due volte. I valori nella sottochiave SharedDlls per il driver Informix sarà come segue:  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```

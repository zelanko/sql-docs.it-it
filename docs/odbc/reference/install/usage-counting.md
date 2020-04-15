---
title: Conteggio dell'utilizzo Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d516a591bfde47522c0ccfe08bd2bd706218e07
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296021"
---
# <a name="usage-counting"></a>Conteggio utilizzi
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare ODBC in modo esplicito solo nelle versioni precedenti di Windows.  
  
 Nel Registro di sistema vengono mantenuti due tipi di conteggi di utilizzo per ogni componente: un conteggio di utilizzo dei componenti e uno o più conteggi di utilizzo dei file facoltativi. Il conteggio dell'utilizzo dei componenti consente alla DLL del programma di installazione di gestire le voci del Registro di sistema. Viene archiviato nel valore UsageCount nelle sottochiavi ODBC Core, driver e traduttore. Per il formato del valore UsageCount e ulteriori informazioni su queste sottochiavi, vedere [Voci del Registro di sistema per](../../../odbc/reference/install/registry-entries-for-odbc-components.md)i componenti ODBC .  
  
 Quando un componente viene installato per la prima volta, la DLL del programma di installazione crea una sottochiave per tale componente e imposta su 1 i dati per il valore UsageCount in tale sottochiave. Quando il componente viene installato nuovamente, la DLL del programma di installazione incrementa il conteggio di utilizzo. Quando il componente viene rimosso, la DLL del programma di installazione decrementa il conteggio di utilizzo. Se il conteggio di utilizzo scende a 0, la DLL del programma di installazione rimuove la sottochiave per il componente.  
  
> [!CAUTION]  
>  Un'applicazione non deve rimuovere fisicamente i file di Driver Manager quando il conteggio di utilizzo dei componenti e il conteggio di utilizzo dei file raggiungono zero.  
  
 I conteggi di utilizzo dei file consentono di determinare quando un file deve essere effettivamente copiato o eliminato anziché incrementare o diminuire il conteggio di utilizzo. Questo è importante perché i componenti ODBC, e quindi i file nei componenti ODBC, sono condivisi e possono essere installati o rimossi da una varietà di applicazioni. L'applicazione può eliminare i file di driver e traduttori se il conteggio di utilizzo dei componenti e il conteggio dell'utilizzo dei file raggiungono zero. I file di Gestione Driver non devono tuttavia essere eliminati quando sia il conteggio di utilizzo dei componenti che il conteggio di utilizzo dei file hanno raggiunto lo zero, perché questi file possono essere utilizzati da altre applicazioni che non hanno incrementato il conteggio di utilizzo dei file.  
  
> [!NOTE]  
>  I conteggi di utilizzo dei file sono facoltativi in Microsoft® WindowsNT® Windows2000.  
  
 I conteggi di utilizzo dei file vengono gestiti dal programma di installazione dopo aver chiamato **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLInstallTranslatorEx**, **SQLRemoveDriverManager**, **SQLRemoveDriver**o **SQLRemoveTranslator**.  
  
 Quando un componente viene installato per la prima volta, il programma di installazione o la DLL del programma di installazione crea un valore nella seguente chiave per ogni file in quel componente che non è già presente nel sistema:  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  Software  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  Shareddlls  
  
 Imposta i dati per tali valori su 1 e copia il file nel sistema. Quando il componente viene installato nuovamente, il programma di installazione o la DLL del programma di installazione incrementa i conteggi di utilizzo. Quando il componente viene rimosso, il programma di installazione o la DLL del programma di installazione decrementa i conteggi di utilizzo. Se il numero di utilizzo scende a 0, il programma di installazione o la DLL del programma di installazione rimuove il valore per il file e, se il componente è un driver o un traduttore, elimina il file. I file di Gestione Driver non devono essere eliminati.  
  
 Il formato del valore del conteggio di utilizzo dei file è illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|*percorso completo*|REG_DWORD|*count*|  
  
 Si supponga, ad esempio, che un driver per Informix utilizzi i file Infrmx32.dll e Infrmx32.hlp e supponiamo che il driver sia stato installato due volte. I valori nella sottochiave SharedDlls per il driver Informix sarebbero i seguenti:  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```

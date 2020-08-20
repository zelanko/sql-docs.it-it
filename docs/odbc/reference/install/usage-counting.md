---
description: Conteggio utilizzi
title: Conteggio dell'utilizzo | Microsoft Docs
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
ms.openlocfilehash: 8e8c02aae51c47b13970a1824e3c0c9c417eb5f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499694"
---
# <a name="usage-counting"></a>Conteggio utilizzi
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare solo in modo esplicito ODBC nelle versioni precedenti di Windows.  
  
 Due tipi di conteggi di utilizzo vengono mantenuti nel registro di sistema per ogni componente: un conteggio di utilizzo del componente e uno o più conteggi di utilizzo file facoltativi. Il conteggio utilizzo componenti consente alla DLL del programma di installazione di gestire le voci del registro. Viene archiviato nel valore UsageCount nelle sottochiavi ODBC core, driver e Translator. Per il formato del valore UsageCount e ulteriori informazioni su queste sottochiavi, vedere [voci del registro di sistema per i componenti ODBC](../../../odbc/reference/install/registry-entries-for-odbc-components.md).  
  
 Quando un componente viene installato per la prima volta, la DLL del programma di installazione crea una sottochiave per l'oggetto e imposta i dati per il valore UsageCount nella sottochiave su 1. Quando il componente viene installato nuovamente, la DLL del programma di installazione incrementa il numero di utilizzi. Quando il componente viene rimosso, la DLL del programma di installazione decrementa il conteggio dell'utilizzo. Se il conteggio di utilizzo è pari a 0, la DLL del programma di installazione rimuove la sottochiave per il componente.  
  
> [!CAUTION]  
>  Un'applicazione non deve rimuovere fisicamente i file di gestione driver quando il conteggio utilizzo componenti e il conteggio utilizzo file raggiungono lo zero.  
  
 I conteggi di utilizzo dei file consentono di determinare quando un file deve essere effettivamente copiato o eliminato anziché incrementare o decrementare il numero di utilizzi. Questo aspetto è importante perché i componenti ODBC e pertanto i file nei componenti ODBC sono condivisi e possono essere installati o rimossi da un'ampia gamma di applicazioni. L'applicazione può eliminare i file di driver e di conversione se il numero di utilizzo del componente e il conteggio di utilizzo dei file raggiungono zero. Tuttavia, i file di gestione driver non devono essere eliminati quando sia il conteggio di utilizzo del componente che il conteggio di utilizzo file hanno raggiunto lo zero, perché questi file possono essere usati da altre applicazioni che non hanno incrementato il numero di utilizzo del file.  
  
> [!NOTE]  
>  I conteggi di utilizzo dei file sono facoltativi in Microsoft® WindowsNT®/Windows2000.  
  
 I conteggi di utilizzo dei file vengono gestiti dal programma di installazione dopo aver chiamato **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLInstallTranslatorEx**, **SQLRemoveDriverManager**, **SQLRemoveDriver**o **SQLRemoveTranslator**.  
  
 Quando un componente viene installato per la prima volta, il programma di installazione o la DLL del programma di installazione crea un valore con la chiave seguente per ogni file in quel componente che non è già presente nel sistema:  
  
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
  
 Imposta i dati per tali valori su 1 e copia il file nel sistema. Quando il componente viene installato nuovamente, il programma di installazione o la DLL del programma di installazione incrementa i conteggi di utilizzo. Quando il componente viene rimosso, il programma di installazione o la DLL del programma di installazione decrementano i conteggi di utilizzo. Se un numero di utilizzo è pari a 0, il programma di installazione o la DLL del programma di installazione rimuove il valore per il file e, se il componente è un driver o un convertitore, Elimina il file. I file di gestione driver non devono essere eliminati.  
  
 La tabella seguente illustra il formato del valore conteggio utilizzo file.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|*percorso completo*|REG_DWORD|*count*|  
  
 Si supponga, ad esempio, che un driver per Informix usi i file Infrmx32.dll e Infrmx32. hlp e che il driver sia stato installato due volte. I valori nella sottochiave SharedDlls per il driver Informix sono i seguenti:  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```

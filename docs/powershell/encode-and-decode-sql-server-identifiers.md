---
title: Codificare e decodificare identificatori di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 21e642feba6a2726aa4d5615f6ae508fa33c1694
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67934657"
---
# <a name="encode-and-decode-sql-server-identifiers"></a>Codificare e decodificare identificatori di SLQ Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Gli identificatori delimitati di SQL Server possono contenere caratteri non supportati nei percorsi di Windows PowerShell. È possibile specificare questi caratteri codificando i valori esadecimali.  

> [!NOTE]
> Esistono due moduli SQL Server PowerShell: **SqlServer** e **SQLPS**. Il modulo **SQLPS** è incluso nell'installazione di SQL Server (per la compatibilità con le versioni precedenti), ma non viene più aggiornato. Il modulo PowerShell più aggiornato è il modulo **SqlServer**. Il modulo **SqlServer** contiene versioni aggiornate dei cmdlet di **SQLPS** e include anche nuovi cmdlet per il supporto delle funzionalità SQL più recenti.  
> Le versioni precedenti del modulo **SqlServer***erano* incluse con SQL Server Management Studio (SSMS), ma solo con le versioni 16.x di SQL Server Management Studio. Per usare PowerShell con SSMS 17.0 e versioni successive, è necessario installare il modulo **SqlServer** da PowerShell Gallery.
> Per installare il modulo **SqlServer**, vedere [Installare il modulo PowerShell SqlServer](download-sql-server-ps-module.md).
  
  
I caratteri non supportati nei nomi dei percorsi di Windows PowerShell possono essere rappresentati o codificati come il carattere "%" seguito dal valore esadecimale del modello di bit che rappresenta il carattere, come in " **%** xx". La codifica può sempre essere utilizzata per gestire i caratteri non supportati nei percorsi di Windows PowerShell.  
  
 Il cmdlet **Encode-SqlName** accetta come input un identificatore di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Viene restituita una stringa con tutti i caratteri non supportati dal linguaggio di Windows PowerShell codificati con "% xx". Il cmdlet **Decode-SqlName** accetta come input un identificatore di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] codificato e restituisce l'identificatore originale.  
  
##  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 I cmdlet **Encode-Sqlname** e **Decode-Sqlname** codificano o decodificano solo i caratteri consentiti negli identificatori delimitati di SQL Server, ma non sono supportati nei percorsi di PowerShell. Di seguito sono elencati i caratteri codificati da **Encode-SqlName** e decodificati da **Decode-SqlName**:  
  
|||||||||||||  
|-|-|-|-|-|-|-|-|-|-|-|-|  
|**Carattere**|\ |/|:|%|\<|>|*|?|[|]|&#124;|  
|**Codifica esadecimale**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|  
  
##  <a name="encoding-an-identifier"></a><a name="EncodeIdent"></a> Codifica di un identificatore  
 **Per codificare un identificatore di SQL Server in un percorso di PowerShell**  
  
-   Utilizzare uno dei due metodi per codificare un identificatore di SQL Server:  
  
    -   Specificare il codice esadecimale per il carattere non supportato utilizzando la sintassi% XX, dove XX rappresenta il codice esadecimale.  
  
    -   Passare l'identificatore come stringa tra virgolette al cmdlet **Encode-Sqlname**  
  
### <a name="examples-encoding"></a>Esempi (codifica)  
 In questo esempio viene specificata la versione codificata del carattere ":" (% 3A):  
  
```  
Set-Location Table%3ATest  
```  
  
 In alternativa, è possibile usare **Encode-SqlName** per compilare un nome supportato da Windows PowerShell:  
  
```  
Set-Location (Encode-SqlName "Table:Test")  
```  
  
##  <a name="decoding-an-identifier"></a><a name="DecodeIdent"></a> Decodifica di un identificatore  
 **Per decodificare un identificatore di SQL Server da un percorso di PowerShell**  
  
 Usare il cmdlet **Decode-Sqlname** per sostituire le codifiche esadecimali con i caratteri rappresentati dalla codifica.  
  
### <a name="examples-decoding"></a>Esempi (decodifica)  
 In questo esempio viene restituito "Table:Test":  
  
```  
Decode-SqlName "Table%3ATest"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Identificatori di SQL Server in PowerShell](sql-server-identifiers-in-powershell.md)   
 [Provider PowerShell per SQL Server](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  

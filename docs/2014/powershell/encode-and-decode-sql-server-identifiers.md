---
title: Codificare e decodificare identificatori di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 46dbf6654b557d612bac6dd2b2a79da114603414
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "64775065"
---
# <a name="encode-and-decode-sql-server-identifiers"></a>Codificare e decodificare identificatori di SQL Server
  Gli identificatori delimitati di SQL Server possono contenere caratteri non supportati nei percorsi di Windows PowerShell. È possibile specificare questi caratteri codificando i valori esadecimali.  
  
1.  **Prima di iniziare:**  [Limitazioni e restrizioni](#LimitationsRestrictions)  
  
2.  **Per elaborare caratteri speciali:**  [Codifica di un identificatore](#EncodeIdent), [decodifica un identificatore](#DecodeIdent)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 I caratteri non supportati nei nomi dei percorsi di Windows PowerShell possono essere rappresentati o codificati come il carattere "%" seguito dal valore esadecimale del modello di bit che rappresenta il carattere, come in " **%** xx". La codifica può sempre essere utilizzata per gestire i caratteri non supportati nei percorsi di Windows PowerShell.  
  
 Il cmdlet **Encode-SqlName** accetta come input un identificatore di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Viene restituita una stringa con tutti i caratteri non supportati dal linguaggio di Windows PowerShell codificati con "% xx". Il cmdlet **Decode-SqlName** accetta come input un identificatore di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] codificato e restituisce l'identificatore originale.  
  
###  <a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 Nei cmdlet `Encode-Sqlname` e `Decode-Sqlname` è possibile codificare o decodificare solo i caratteri consentiti negli identificatori delimitati di SQL Server, ma non sono supportati nei percorsi di PowerShell. Caratteri codificati da **Encode-SqlName** e decodificati da **Decode-SqlName**:  
  
|||||||||||||  
|-|-|-|-|-|-|-|-|-|-|-|-|  
|**Carattere**|\ |/|:|%|\<|>|*|?|[|]|&#124;|  
|**Codifica esadecimale**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|  
  
##  <a name="EncodeIdent"></a> Codifica di un identificatore  
 **Per codificare un identificatore di SQL Server in un percorso di PowerShell**  
  
-   Utilizzare uno dei due metodi per codificare un identificatore di SQL Server:  
  
    -   Specificare il codice esadecimale per il carattere non supportato utilizzando la sintassi% XX, dove XX rappresenta il codice esadecimale.  
  
    -   Passare l'identificatore come stringa tra virgolette al cmdlet `Encode-Sqlname`  
  
### <a name="examples-encoding"></a>Esempi (codifica)  
 In questo esempio viene specificata la versione codificata del carattere ":" (% 3A):  
  
```  
Set-Location Table%3ATest  
```  
  
 In alternativa, è possibile usare **Encode-SqlName** per compilare un nome supportato da Windows PowerShell:  
  
```  
Set-Location (Encode-SqlName "Table:Test")  
```  
  
##  <a name="DecodeIdent"></a> Decodifica di un identificatore  
 **Per decodificare un identificatore di SQL Server da un percorso di PowerShell**  
  
 Utilizzare il cmdlet `Decode-Sqlname` per sostituire le codifiche esadecimali con i caratteri rappresentati dalla codifica.  
  
### <a name="examples-decoding"></a>Esempi (decodifica)  
 In questo esempio viene restituito "Table:Test":  
  
```  
Decode-SqlName "Table%3ATest"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Identificatori di SQL Server in PowerShell](sql-server-identifiers-in-powershell.md)   
 [Provider PowerShell per SQL Server](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  

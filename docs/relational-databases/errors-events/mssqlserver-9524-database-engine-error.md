---
title: MSSQLSERVER_9524 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9524 (Database Engine error)
ms.assetid: 12da7931-e124-4466-889c-046f1b7b7bfd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 40c707873679d2e5d166f2c1319f971404deabe5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "67903843"
---
# <a name="mssqlserver_9524"></a>MSSQLSERVER_9524
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|9254|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|XMLERR_INVALID_COLUMNSET_XML|  
|Testo del messaggio|Il contenuto XML fornito non è conforme al formato XML richiesto per i set di colonne di tipo sparse.|  
  
## <a name="explanation"></a>Spiegazione  
È stato eseguito il tentativo di modificare un set di colonne. Il contenuto XML di un set di colonne deve soddisfare le restrizioni del formato relativo. Il formato generale di un set di colonne è il seguente:  
  
`<column_name_1>value1</column_name_1><column_name_2>value2</column_name_2>...`  
  
Per ulteriori informazioni sui set di colonne, vedere l'argomento "Utilizzo di set di colonne" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-action"></a>Azione dell'utente  
Correggere il formato del codice XML per il set di colonne nell'istruzione.  
  

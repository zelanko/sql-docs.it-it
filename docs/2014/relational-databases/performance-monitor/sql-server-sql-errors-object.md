---
title: Oggetto SQL Errors di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQL Errors object
- SQLServer:SQL Errors
ms.assetid: 6e5273ca-29cb-4618-88a2-70b9b8d6cf76
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f36cd694756544a44df657d97fd84e1967167b55
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63183013"
---
# <a name="sql-server-sql-errors-object"></a>Oggetto Errori SQL di SQL Server
  L'oggetto **SqlServer: errori SQL** di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce contatori per il monitoraggio degli **errori SQL**.  
  
 Nella tabella seguente sono illustrati i contatori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Errori SQL** .  
  
|Contatori dell'oggetto Errori SQL di SQLServer|Descrizione|  
|------------------------------------|-----------------|  
|**Errori/sec**|Numero di errori/sec|  
  
 Per ogni contatore nell'oggetto sono disponibili le istanze seguenti:  
  
|Elemento|Definizione|  
|----------|----------------|  
|**_Total**|Informazioni relative a tutti gli errori.|  
|**Errori offline del database**|Tiene traccia degli errori gravi che obbligano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a impostare il database corrente come offline.|  
|**Informazioni sugli errori**|Informazioni relative a messaggi di errore di tipo informativo che non provocano errori.|  
|**Elimina errori di connessione**|Tiene traccia degli errori gravi che obbligano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a terminare la connessione corrente.|  
|**Errori utente**|Informazioni sugli errori dell'utente.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  

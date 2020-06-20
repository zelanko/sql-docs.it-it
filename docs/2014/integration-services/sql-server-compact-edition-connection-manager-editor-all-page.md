---
title: Editor gestione connessione SQL Server Compact Edition (pagina tutti) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlmobileconnection.all.f1
helpviewer_keywords:
- SQL Server Compact Connection Manager Editor
ms.assetid: f9fbff4b-c502-44b3-8e7b-398d66e82206
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9e6b326e86e1a9e21a740c3bf1bd1fedb6919e98
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84962734"
---
# <a name="sql-server-compact-edition-connection-manager-editor-all-page"></a>Editor gestione connessione SQL Server Compact Edition (pagina Tutte)
  Utilizzare la finestra di dialogo **Editor gestione connessione SQL Server Compact Edition** per specificare le proprietà di connessione a un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 Per ulteriori informazioni sulla gestione connessione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact Edition, vedere [Editor gestione connessione SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md).  
  
## <a name="options"></a>Opzioni  
 **AutoShrink Threshold**  
 Consente di specificare la quantità di spazio libero in percentuale consentito nel database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact al raggiungimento della quale verrà avviata l'operazione di compattazione automatica.  
  
 **Default Lock Escalation**  
 Consente di specificare il numero di blocchi di database acquisiti dal database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact prima di tentare l'escalation.  
  
 **Default Lock Timeout**  
 Consente di specificare l'intervallo di tempo predefinito (in millisecondi) per cui una transazione deve rimanere in attesa di un blocco.  
  
 **Flush Interval**  
 Consente di specificare l'intervallo di tempo (in secondi) dopo il quale le transazioni completate devono essere scaricate su disco.  
  
 **Locale Identifier**  
 Consente di specificare l'ID delle impostazioni locali (LCID) del database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Max Buffer Size**  
 Consente di specificare la quantità massima di memoria in KB usata da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact al raggiungimento della quale viene eseguito lo scaricamento dei dati su disco.  
  
 **Dimensioni massime del database**  
 Consente di specificare le dimensioni massime in MB del database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Modalità**  
 Consente di specificare la modalità file in cui aprire il database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact. Il valore predefinito di questa proprietà è **Read Write**.  
  
 Nella tabella seguente sono descritti i quattro valori disponibili per la proprietà Mode.  
  
|valore|Description|  
|-----------|-----------------|  
|**Sola lettura**|Imposta l'accesso di sola lettura al database.|  
|**Lettura/scrittura**|Imposta l'autorizzazione di lettura/scrittura per il database.|  
|**Exclusive**|Imposta l'accesso esclusivo al database.|  
|**Shared Read**|Specifica che altri utenti possono accedere contemporaneamente in lettura al database.|  
  
 **Persist Security Info**  
 Consente di specificare se le informazioni di sicurezza vengono restituite all'interno della stringa di connessione. Il valore predefinito dell'opzione è **False**.  
  
 **Temp File Directory**  
 Consente di specificare il percorso del file di database temporaneo di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Origine dati**  
 Consente di specificare il nome del database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Password**  
 Consente di immettere la password per il database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor gestione connessione SQL Server Compact Edition &#40;pagina Connessione&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
  

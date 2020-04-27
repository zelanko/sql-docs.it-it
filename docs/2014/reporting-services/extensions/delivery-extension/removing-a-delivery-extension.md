---
title: Rimozione di un'estensione per il recapito | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7c4320f46b5013b0fa2accbc81792748c2d9f384
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63164010"
---
# <a name="removing-a-delivery-extension"></a>Rimozione di un'estensione per il recapito
  Per rimuovere un'estensione per il recapito di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], rimuovere semplicemente l'elemento **Extension** per l'estensione dal file di configurazione. Dopo la rimozione delle informazioni di configurazione, l'estensione per il recapito non è più disponibile per il server di report.  
  
 Dopo aver rimosso l'elemento **Extension** corrispondente di un'estensione per il recapito dal file di configurazione, l'estensione non è più registrata nel server di report. Il server di report rimuove la voce dall'elenco di estensioni per il recapito e disattiva qualsiasi sottoscrizione che utilizza tale estensione. Quando un'estensione per il recapito viene rimossa, gli utenti non possono più selezionarla come metodo di notifica.  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di un'estensione per il recapito](implementing-a-delivery-extension.md)   
 [Libreria di estensioni di Reporting Services](../reporting-services-extension-library.md)  
  
  

---
title: Classe SqlServerAlias | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- SqlServerAlias Class
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SqlServerAlias class
ms.assetid: 475662b9-6985-45bf-b1e9-b0f26ef50443
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0ffbf733db8cbd672f171773e7b44560686e7d1a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63223551"
---
# <a name="sqlserveralias-class"></a>Classe SqlServerAlias
  La [classe SqlServerAlias](sqlserveralias-class.md) rappresenta un alias di connessione al server.  
  
 È necessario un alias di connessione al server quando si verificano le seguenti condizioni:  
  
-   Il client si connette a un'istanza di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] su un trasporto di rete diverso da quello predefinito.  
  
-   L'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a cui è connesso il client è in attesa su una named pipe alternativa.  
  
 **Nota:** Il [classe SqlServerAlias](sqlserveralias-class.md) eredita il `Put` metodo dalla classe Provider. Tuttavia, non viene restituito alcun risultato come indicato dal metodo `Provider::Put`. Per ulteriori informazioni, vedere la documentazione di WMI.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli client](https://technet.microsoft.com/library/ms181035.aspx)  
  
  

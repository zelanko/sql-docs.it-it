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
ms.openlocfilehash: 46994409cc6a5119c9144eb7a3a4b9a8a9a22c44
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85002450"
---
# <a name="sqlserveralias-class"></a>Classe SqlServerAlias
  La [classe SqlServerAlias](sqlserveralias-class.md) rappresenta un alias di connessione al server.  
  
 È necessario un alias di connessione al server quando si verificano le seguenti condizioni:  
  
-   Il client si connette a un'istanza di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] su un trasporto di rete che non è il trasporto di rete predefinito.  
  
-   L'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a cui è connesso il client è in attesa su una named pipe alternativa.  
  
 **Nota:** La [classe SqlServerAlias](sqlserveralias-class.md) eredita il `Put` Metodo dalla classe provider. Tuttavia, non viene restituito alcun risultato come indicato dal metodo `Provider::Put`. Per ulteriori informazioni, vedere la documentazione di WMI.  
  
## <a name="see-also"></a>Vedere anche  
 [configurazione di protocolli client](https://technet.microsoft.com/library/ms181035.aspx)  
  
  

---
title: ConnectPromptEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 40ce74748e15a2715de26e813007e00be0c33729
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698605"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
Specifica se una finestra di dialogo deve essere visualizzata per la richiesta di parametri mancanti quando si apre una connessione a un'origine dati.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|Richiede sempre.|  
|**adPromptComplete**|2|Viene richiesto se sono necessarie ulteriori informazioni.|  
|**adPromptCompleteRequired**|3|Viene richiesto se sono necessarie ulteriori informazioni, ma non sono consentiti parametri facoltativi.|  
|**adPromptNever**|4|Mai richieste.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.ConnectPrompt.ALWAYS|  
|AdoEnums.ConnectPrompt.COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums.ConnectPrompt.NEVER|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà dinamica Prompt (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)

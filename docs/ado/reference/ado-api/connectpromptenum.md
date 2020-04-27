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
ms.openlocfilehash: afd5d9ca0de6b8d2ffba75f862e6ca0afb594848
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67919449"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
Specifica se deve essere visualizzata una finestra di dialogo per richiedere parametri mancanti quando si apre una connessione a un'origine dati.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|Richiede sempre.|  
|**adPromptComplete**|2|Richiede se sono necessarie altre informazioni.|  
|**adPromptCompleteRequired**|3|Richiede se sono necessarie altre informazioni ma non sono consentiti parametri facoltativi.|  
|**adPromptNever**|4|Non richiede mai.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. ConnectPrompt. ALWAYs|  
|AdoEnums. ConnectPrompt. COMPLETE|  
|AdoEnums. ConnectPrompt. COMPLETEREQUIRED|  
|AdoEnums. ConnectPrompt. NEVER|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà dinamica Prompt (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)

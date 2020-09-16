---
description: Proprietà DatabaseQueryTimeout (MSReportServer_ConfigurationSetting WMI)
title: Proprietà DatabaseQueryTimeout (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- DatabaseQueryTimeout Property
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DatabaseQueryTimeout property
ms.assetid: 96faed97-9799-4bbf-a66f-fdd532d3eace
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5772326704b5e5fd6861b6185dab75cefdf42d1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472633"
---
# <a name="configurationsetting-property---databasequerytimeout"></a>Proprietà di ConfigurationSetting - DatabaseQueryTimeout
  Specifica il numero di secondi di attesa prima che il server di report presuma che il comando non sia riuscito e che sia necessaria una quantità di tempo troppo elevata per l'esecuzione. Il server di report calcola il tempo di esecuzione della query rispetto al catalogo SQL e non rispetto a un'origine dati per il report. Proprietà di lettura/scrittura.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Dim DatabaseQueryTimeout As UInt32  
```  
  
```csharp  
public UInt32 DatabaseQueryTimeout;  
```  
  
## <a name="property-values"></a>Valori della proprietà  
 Oggetto **integer** non firmato a 32 bit che rappresenta il numero di secondi concessi per l'esecuzione della query.  
  
## <a name="example-code"></a>Codice di esempio  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
